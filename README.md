# NgAudio

Library to visualize audio waveform. Built as pure Angular library that doesn't wrap any of JS library. With NgWaveform you can create interactive customisable waveform of any audio file in your Angular application.

## Quick start
```bash
npm install --save @billen/ng-waveform
```

```typescript
import { ITimeUpdateEvent, NgWaveformComponent, IRegionPositions } from 'ng-waveform';

@ViewChild('waveform', { static: false }) waveform: NgWaveformComponent;

onPlayButtonClick() {
  this.waveform.play();
}
onPauseButtonClick() {
  this.waveform.pause();
}
```

```html
<ng-waveform #waveform class="waveform"
    [src]="src"
    [height]="150"
    [useRegion]="true"
    backgroundColor="#d3d3d3"
    regionBackgroundColor="rgba(255, 255, 255, 0.7)"
    regionStartStickColor="#21f032"
    [markers]="[]"
    markerColor="#096"
    regionEndStickColor="red"
    regionTextColor="#09417e"
    [withRegionLabels]="true"
    waveColor="#ff11ff"
    (trackLoaded)="onTrackLoaded($event)"
    (rendered)="onTrackRendered($event)"
    (durationChange)="onDurationChange($event)"
    (timeUpdate)="onTimeUpdate($event)"
    (paused)="onPaused()"
    (regionChange)="onRegionChange($event)"
  >
</ng-waveform>
```

## API Reference
`NgWaveformComponent`


### Methods
* `play(start: number = 0): void`
Play audio, start - starting position

* `pause(): void`
Stops audio

### Events
* `trackLoaded` - emits when data fetched from Url, returns time in ms spent for fetching.
* `rendered` - emits when waveform is rendered, returns time in ms spent for rendering.
* `durationChange` - emits when duration of audio is changed, returns duration value in seconds.
* `timeUpdate` - emits when current time of audio changes, returns object that implements interface `ITimeUpdateEvent`.
* `paused` - emits when audio paused. Useful for switch Play/Pause buttons in external control.
* `regionChange` - emits when region start or/and end positions change, returns object that implements interface `IRegionPositions`.


### Properties
Name | Description
-------------|------------
`src: string` | Url of src mp3 file
`height = 100` | Height of component
`waveColor = '#d3d3d3'` | Color of wave
`backgroundColor = 'transparent'` | Background color of component
`overlayBackgroundColor = 'rgba(0, 0, 0, 0.5)'` | Background color of overlay filling component while playing
`useRegion: boolean` | Turn region on
`withRegionLabels: boolean` | Turn region labels on
`regionBackgroundColor = 'transparent'` | Background color of region
`regionStartStickColor = 'red'` | Color of region left border stick
`regionEndStickColor = 'red'` | Color of region right border stick
`regionTextColor = '#000'` | Color of region labels text
`autoplay` | Turn autoplay on load on
`markers` | Adds a lined marker at those locations to point out a specific time within the track
`markerColor` | Which color would you like the markers to be. Preferably you want a constrasting one relative to the waveColor property 

### Intrfaces
```typescript
interface ITimeUpdateEvent {
  time: number;
  progress: number;
}
```

```typescript
interface IRegionPositions {
  start: number;
  end: number;
}
```

Currently only the time is being used to indicate a marker.

```typescript
interface Marker {
  time: number;
  label: string;
}
```

### Credits
Thank you very much for the original repository from [Arthur Groupp](https://github.com/agroupp/ng-waveform).

Thank you very much for great inspiration [wavesurfer.js](https://wavesurfer-js.org/) team.

### Conclusion
Feedback, issues and stars will be very appreciated.
