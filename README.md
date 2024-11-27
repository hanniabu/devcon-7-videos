# devcon-7-videos

1. Load https://www.youtube.com/@EthereumFoundation/videos
2. Scroll down to the start of the devcon videos
3. Open the browser console and run the following snippet:
   ```
    let devconVideos = [];
    document.querySelectorAll('#details #meta').forEach(function(video) {
    	let link = video.querySelector('#video-title-link').href;
    	let title = video.querySelector('#video-title').innerText;
    	let views = video.querySelectorAll('#metadata-line .inline-metadata-item')[0].innerText;
    	views = views.toLowerCase().replace('views','').replace('view','').replace('k','000').trim();
    	views = Number(views);
    	let age = video.querySelectorAll('#metadata-line .inline-metadata-item')[1].innerText;
    	let markdown = `[${title} (${views} views, ${age})](${link})`
    	if (!age.includes('year') && !age.includes('month')) {
    		devconVideos.push({'link':link,'title':title,'views':views,'age':age,'markdown':markdown});
    	}
    })
    let devconVideosSorted = devconVideos.sort((a, b) => b.views - a.views);
    console.log(devconVideosSorted);
    console.log(devconVideosSorted.length);
   ```
4. This results in a json array sorted by most views: https://github.com/hanniabu/devcon-7-videos/blob/main/videos.json
5. From that you can derive a markdown list sorted by most views: https://github.com/hanniabu/devcon-7-videos/blob/main/videos.md
