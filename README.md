# Player Queue
Using the MediaPlayer framework, you can do some great things with the system's music player like playing music, getting song information, and more. You can also append, prepend, and set the system music player's queue which is great in theory, but in reality can be very difficult to use, especially for beginners.
 
Thankfully, I've figured out how to use the complicated system queue system so you don't have to. Let's shut up and get straight to the code.

## Download the Class
I've created a very easy-to-use class called `PlayerQueue` to control the Apple Music Queue. You can download it, here.


## Setting Up
Download the class as mentioned above, add it to your Xcode project, and then use the `PlayerQueue` wherever you'd like. In this example, we're going to use a `UIViewController`. Just create an instance of the class, and now you're ready to use it!
```
class MainController: UIViewController {
   override func viewDidLoad() {
      var playerQueue = PlayerQueue()
   }
}
```

## Getting the Catalog IDs
There are three ids when using Apple Music, we have the Catalog ID, Store ID, and Library ID. Although, Catalog IDs and Store IDs are the same things, just called different things throughout Apple's frameworks and APIs. In this tutorial, we'll call them Catalog IDs. In addition to this, for this tutorial, we'll be focusing on Catalog/Store IDs although I plan on extending my class for Library IDs in the future. You can get the Catalog ID(s) one of two ways:

**Apple Music API:** You can get the Catalog IDs by making requests to the [Apple Music API](https://developer.apple.com/documentation/applemusicapi/). For the simplicity of this tutorial, we won't get into all of that however there are many tutorials teaching how to use the API. 
**systemMusicPlayer:** Using the [MediaPlayer](https://developer.apple.com/documentation/mediaplayer/) framework, Catalog IDs can be easily found using the system music player. For example, let's get the id from the now playing song.

```
import MediaPlayer 
class MainController: UIViewController {
   let player = MPMusicPlayerController.systemMusicPlayer
   override func viewDidLoad() {
      var playerQueue = PlayerQueue()
      if let song = player.nowPlayingItem {
         let id = song?.playbackStoreID
      }
   }
}
```
The IDs you return should look something like the ones bellow. For this tutorial, we'll be using these. For testing purposes, you can as well.
```
let idArray = ["1547316386", "1547316394", "1547316698"]
let id = "1547316386"
```
Now, let's get to actually using PlayerQueue.

## Prepend to Queue
This adds song(s) to the beginning of the queue. You can either prepend an array of catalog ids
```
playerQueue.prepend(ids: idArray)
```
…or you can prepend a single catalog id
```
playerQueue.prepend(id: id)
```

## Append to Queue
This adds song(s) to the end of the queue. Just like prepend, you can either append an array of catalog ids
```
playerQueue.append(ids: idArray)
```
…or you can append a single catalog id
```
playerQueue.append(id: id)
```

## Set the Queue
This removes any songs that were in the queue and replaces them with your new songs
```
playerQueue.setQueue(ids: idArray)
```

## Play All
This plays all the songs in an array of ids. Staring with the first and prepending the rest to the queue.
```
playerQueue.playAll(ids: idArray)
```

## Shuffle All
This shuffles all the songs in an array of song ids. Staring with the first and prepending the rest to the queue
```
playerQueue.shuffleAll(ids: idArray)
```

And that's it! Sadly, we cannot read the queue from the system music player, we can only prepend, append, and set. You can do this, however using an [applicationQueuePlayer](https://developer.apple.com/documentation/mediaplayer/mpmusicplayercontroller/2817540-applicationqueueplayer/). As I mentioned before, I plan on updating this tutorial for Library IDs returned by the Apple Music API so stay on the lookout for that!
