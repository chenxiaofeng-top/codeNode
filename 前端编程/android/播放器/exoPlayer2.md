ExoPlayer需要的元素（组成）

```groovy
//版本,与最新版本不兼容
implementation 'com.google.android.exoplayer:exoplayer:2.13.2'
```

- 播放器内核 SimpleExoPlayer
- 视图 PlayerView
- 播放源处理器 MediaItem
- 监听事件

代码：

```java
package com.jinuofan.component.videoView;

import android.content.Context;
import android.util.AttributeSet;
import android.widget.FrameLayout;

import com.google.android.exoplayer2.MediaItem;
import com.google.android.exoplayer2.Player;
import com.google.android.exoplayer2.SimpleExoPlayer;
import com.google.android.exoplayer2.ui.AspectRatioFrameLayout;
import com.google.android.exoplayer2.ui.PlayerView;
import com.jinuofan.component.videoView.inf.VideoPlayer;

/**
 * 封装SimpleExoPlayer
 */
public class ExoVideoPlayer extends PlayerView implements VideoPlayer {

    private static final String TAG = "VideoPlayer";

    public static final String STATE_PLAYING = "playing";
    public static final String STATE_PAUSE = "pause";
    public static final String STATE_STOP = "stop";
    public static final String STATE_BUFFERING = "buffering";
    public static final String STATE_ENDED = "ended";
    /**
     * 播放状态
     */
    public String state;

    private SimpleExoPlayer player;

    public ExoVideoPlayer(Context context) {
        super(context);
        init(context);
    }

    public ExoVideoPlayer(Context context, AttributeSet attrs) {
        super(context, attrs);
        init(context);
    }

    public ExoVideoPlayer(Context context, AttributeSet attrs, int defStyleAttr) {
        super(context, attrs, defStyleAttr);
        init(context);
    }

    private void init(Context context) {

        player = new SimpleExoPlayer.Builder(context).build();
        this.setPlayer(player);
        //是否要显示进度条，
        this.setUseController(false);
        this.setResizeMode(AspectRatioFrameLayout.RESIZE_MODE_FILL);
    }


    @Override
    public void play(String url, int x, int y, int width, int height) {
        FrameLayout.LayoutParams layoutParams = (LayoutParams) this.getLayoutParams();
        layoutParams.width = width;
        layoutParams.height = height;
        layoutParams.leftMargin = x;
        layoutParams.topMargin = y;
        setLayoutParams(layoutParams);

        MediaItem mediaItem = MediaItem.fromUri(url);
        player.setMediaItem(mediaItem);
        player.prepare();
        player.play();
    }

    @Override
    public void stop() {
        player.stop();
        state = STATE_STOP;
    }

    @Override
    public void pause() {
        player.pause();
        state = STATE_PAUSE;
    }

    @Override
    public void resume() {
        player.play();
    }

    @Override
    public void seek(long position) {
        player.seekTo(position);
    }

    @Override
    public void setVolume(float volume) {
        player.setVolume(volume);
    }

    @Override
    public float getVolume() {
        return player.getVolume();
    }

    @Override
    public void setSilence() {
        player.setDeviceMuted(true);
    }

    @Override
    public void cancelSilence() {
        player.setDeviceMuted(false);
    }

    @Override
    public boolean isSilence() {
        return player.isDeviceMuted();
    }

    @Override
    public long getDuration() {
        return player.getDuration();
    }

    @Override
    public long getCurrentPosition() {
        return player.getCurrentPosition();
    }

    @Override
    public String getPlayState() {
        int playbackState = player.getPlaybackState();
        if (playbackState == Player.STATE_BUFFERING) {
            return STATE_BUFFERING;
        }
        if (playbackState == Player.STATE_ENDED) {
            return STATE_ENDED;
        }

        if (player.isPlaying()) {
            return STATE_PLAYING;
        }

        return state;
    }

    @Override
    public void release() {
        player.release();
        player=null;
    }
}

```

