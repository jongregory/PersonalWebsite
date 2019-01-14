---
title: "Video Indexer"
date: 2018-11-14T13:55:12Z
draft: false
tags: ["azure","ai","cognitive services"]
---

This week I have been looking at a proof of concept using the Microsoft [Video Indexer](https://vi.microsoft.com/en-us/) service. This is a combination service of various azure cognitive services working together to analyse and provide insights on Videos.

As with all the azure cognitive services its an easy tool to pick up, videos can be uploaded via the portal or the [api](https://docs.microsoft.com/en-us/azure/media-services/video-indexer/video-indexer-use-apis). Once videos are uploaded they are analysed and can then be viewed in the portal or extracted from the api. 

When viewing in the portal the videos are available for streaming, with each insight metric linked to the place in the video. The [Video Indexer Tour](https://vi.microsoft.com/en-us/tour) has screen shots of this feature. In a real world application you are likely to want to build your own UI around this and use the information from the Video Indexer API.

The high level features of the service are;

- Facial  Recognition (Detecting, Grouping, Custom Identification, Thumbnail generation)
- Visual Analysis (Text Recognition, Object Identification, Visual Content Moderation)
- Video Analysis (Shot Detection, Black Frame Detection, Keyframe Identification)
- Audio Analysis (Keyword Extraction, Topic Inference, Brand Mentions, Sentiment & Emotion Analysis)
- Speech to Text (Language Identification, Automated Transcription, Captioning, Translation)
- Sound & Voice (Noise Reduction, Speaker Identification, Speaker Stats)

This [blog](https://azure.microsoft.com/en-gb/blog/video-indexer-general-availability-and-beyond/) describes some of the insights available in more detail.

The main feedback from the POC work was the accuracy of speech recognition wasn't as good as a human transcription, it is however a lot cheaper and quicker. The POC used videos with a lot of different accents and languages talking using domain specific vocabulary, this [blog post](https://azure.microsoft.com/en-gb/blog/bring-your-own-vocabulary-to-microsoft-video-indexer/) describes how video indexer can be customised with adaptation text to aid the interpretation of the video text.

The main benefit of a service such as this is the speed and ease of use, if you have video content you want to either analyse for insights or provide greater accessibility to on your website or application. Then this service can be integrated via the api and the video content can be searched and indexed too, not only on the text but also the cognitive understanding. This make searches such as "Videos containing the Prime Minister" or "Videos containing positive reviews of my product x" possible within realistic budgets and timescales.