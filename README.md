This is my edition of [RecordRTC](https://www.npmjs.com/package/recordrtc) package. ([Full Documentation](https://recordrtc.org/))

# Changes
## Audio loose on `resetVideoStreams` method on [RecordRTC.js](https://github.com/muaz-khan/RecordRTC/blob/master/RecordRTC.js)

new code:

```javascript
function resetVideoStreams(streams) {
    videos = [];
    streams = streams || arrayOfMediaStreams;

    // via: @adrian-ber
    streams.forEach(stream => {
        if (stream.getTracks().filter(function (t) {
            return t.kind === 'video';
        }).length) {
            var video = getVideo(stream);
            video.stream = stream;
            videos.push(video);
        }

        if (stream.getTracks().filter(function (t) {
            return t.kind === 'audio';
        }).length && self.audioContext) {
            var audioSource = self.audioContext.createMediaStreamSource(stream);
            audioSource.connect(self.audioDestination);
            self.audioSources.push(audioSource);
        }
    });

}
```

