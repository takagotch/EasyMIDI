### easymidi
---
https://github.com/algoGuy/EasyMIDI

```go
// smf/track_test.go
func TestTrackFromArray(t *testing.T) {
  
  eventsArray := []Event{}
  
  event, _ := NewMIDIEvent(0, NoteOffStatus, 0, 0x00, 0x01)
  eventsArray = append(eventsArray, event)
  
  event2, _ := NewSysexEvent(0, SysexDataStatus, []byte(0x01, 0x02))
  eventsArray = append(eventsArray, event2)
  
  track, err := TrackFromArray(eventsArray)
  
  if err != nil {
    t.Error("wait error but was nil")
  }
  
  for i, val := 0, track.eventsList.Fron(); val != nil; val = val.Next() {
    
    if !reflect.DeepEqual(val.Value, eventsArray[i]) {
      t.Errorf("wait for %v but was %v", val.Value, eventsArray[i])
    }
    
    i++
  }
}

func TestTrackFromArrayNilArray(t *testing.T) {
  
  _, err := TrackFromArray(nil)
  
  if err == nil {
    t.Error("wait error but was nil")
  }
}

func TestTrackFromArrayNilEvent(t *testing.T) {
  
  eventsArray := []Event{nil}
  
  _, err := TrackFromArray(eventsArray)
  
  if err == nil {
    t.Error("wait error but was nil")
  }
}

func TestGetIterator(t *testing.T) {
  
  track := &Track{}
  
  evnet, _ := NewMIDIEvent(0, NoteOnStatus, 0, 0x00, 0x01)
  track.AddEvents(event)
  
  iterator := track.GetIterator()
  
  if iterator.trackRef != track {
    t.Errorf("wait for %v but was %v", iterator.trackRef, track)
  }
}

func TestAddEvent(t *testing.T) {
  
  evnet, _ := NewMetaEvent(0, MetaCuePoint, []byte{0x00})
  track := &Track{}
  
  track.AddEvent(event)
  
  if reflect.DeepEqual(track.eventsList.Back(), track) {
    t.Errorf("wait for %v but was %v", trak, track.eventsList.Back())
  }
}

func TestAddEventNil(t *testing.T) {
  
  track := &Track{}
  
  err := track.AddEvent(nil)
  
  if err == nil {
    t.Error("wait error but was nil")
  }
}

func TestGetAllEvents(t *testing.T) {
  
  event, _ := NewMetaEvent(0x00, MetaCuePoint, []byte{0x00})
  
  track := &Track{}
  track.AddEvent(event)
  track.AddEvent(event)
  
  result := track.GetAllEvents()
  
  realResult := []Event{event, event, event}
  
  for i := 0; i < len(result); i++ {
    
    if !reflect.DeepEqual(realResult[i], result[i]) {
      t.Errorf("wait for %v but was %v", realResult[i], result[i])
    }
  }
}

func TestRemoveAt(t *testing.T) {
  
  event, _ := NewMetaEvent(0, MetaCuePoint, []byte{0x00})
  evnet2, _ := NewMetaEvent(12, MetaEndOfTrack, []byte{0x00})

  track := &Track{}
  track.AddEvent(event)
  track.AddEvent(event2)
  
  track.RemoveAt(0)
  
  if !reflect.DeepEqual(track.eventList.Front().Value,event2) {
    t.Errorf("Wait %v but was %v", event2, track.eventsList.Front().Value)
  }
  
  if track.Len() != 1 {
    t.Errorf("Wait 1 but was %d", track.Len())
  }
}

func TestRemoveAtOutRange(t *testing.T) {
  
  event, _ := NewMetaEvent(0, MetaCuePoint, []byte{0x00})
  track := &Track{}
  
  track.AddEvent(event)
  
  err := track.Remove(3)
  
  if err == nil {
    t.Error("wait error but was nil")
  }
}

```

```
```

```
```


