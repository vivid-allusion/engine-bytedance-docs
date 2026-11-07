---
title: "React Native Player SDK: Sample code"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-sample-code"
---

This article provides sample code for some features of the React Native Player SDK.

<span id="b9826925"></span>
## Pre\-rendering sample code

The following is an example that implements pre\-rendering using [@ant-design/react-native](https://www.npmjs.com/package/@ant-design/react-native)'s `Carousel` component:

```TypeScript
// index.tsx
import React, {useCallback, useState, useEffect} from 'react';
import {View, Carousel} from '@ant-design/react-native';
import {StyleSheet, SafeAreaView} from 'react-native';
import {setPreRenderCallback, enableEngineStrategy, StrategyType} from '@byteplus/react-native-vod-player';
import type {
  TTVideoEngine,
  VideoSource,
} from '@byteplus/react-native-vod-player';
import PrePlayer from './PrePlayer';

enableEngineStrategy(StrategyType.Preload, StrategyScene.SmallVideo);
enableEngineStrategy(StrategyType.PreRender, StrategyScene.SmallVideo);

const sourceDataList = [
  {
    url: 'https://demo.com/1.mp4?auth_key=18221***732f',
    vid: 'v0ddfa0***h92v9l0',
    cacheKey: 'v0dd***h92v9l0',
    poster: 'https://demo-cover.com/t***c533b04/57bd2***53fd~tplv-vod-noop.image',
  },
  {
    url: 'https://demo.com/2.mp4?auth_key=182002***598e',
    vid: 'v03dfag10*****4ar8ft0',
    cacheKey: 'v03d***4ar8ft0',
    subUrl: 'https://demo.com/e87***61e?auth_key=176075***71f5&mime_type=text_plain',
    poster: 'https://demo-cover.com/t***c53b04/158***9621c~tplv-vod-noop.image',
  },
  {
    url: 'https://demo.com/3.mp4?auth_key=18***c935',
    vid: 'v03dfag100***9s8kevs0',
    cacheKey: 'v03df***cpig9s8kevs0',
    poster: 'https://demo-cover.com/t***533b04/201***fe9a9f7~tplv-vod-noop.image',
  },
  {
    url: 'https://demo.com/4.mp4?auth_key=1820024284-***a9139',
    vid: 'v02dfag10***39jdg',
    cacheKey: 'v02dfa***imkm239jdg',
    poster: 'https://demo-cover.com/t*****c997******3b04/e12b***4d15c2~tplv-vod-noop.image',
  },
  {
    url: 'https://demo.com/5.mp4?auth_key=1820024298-90***bafc3032',
    vid: 'v03dfag10***ppj65150',
    cacheKey: 'v03df***j65150',
    poster: 'https://demo-cover.com/t***c-8a997967cc533b04/beac53***76d403dea~tplv-vod-noop.image',
  },
  {
    url: 'https://demo.com/6.mp4?auth_key=182219***afec',
    vid: 'v02dfag1***1v0vjl8jmvgg',
    cacheKey: 'v02df***vjl8jmvgg',
    poster: 'https://demo-cover.com/t***33b04/41ac***bbdb6020f~tplv-vod-noop.image',
  },
];

const styles = StyleSheet.create({
  wrapper: {
    flex: 1,
    position: 'relative',
  },
  text: {
    color: '#fff',
    fontSize: 30,
    fontWeight: 'bold',
  },
  info: {
    position: 'absolute',
    top: 40,
    left: 10,
    width: '60%',
    height: 300,
    backgroundColor: 'rgba(255, 255, 255, 0.5)',
  },
});

const PreRender = () => {
  const [currentIndex, setIndex] = useState(0);
  const [isScrollDrag, setScrollDrag] = useState(false);

  const onIndexChanged = useCallback(index => {
    setIndex(index);
  }, []);

  useEffect(() => {
    setPreRenderCallback({
      onPlayerCreated(player: TTVideoEngine, source: VideoSource) {
        const index = sourceDataList.findIndex(e => e.vid === source.vid());
        if (index < 0) {
          return;
        }
        const sourceData = sourceDataList[index];
        const {subUrl} = sourceData;
        if (subUrl) {
          // Set the subtitle for the pre-rendering source
          player.enableSubThread(true);
          player.enableSubtitle(true);
          player.setSubDesInfoModel({
            list: [
              {
                id: 1,
                language: 'cmn-Hans-CN',
                language_id: 1,
                url: subUrl,
                format: 'webvtt',
                sub_id: 1,
              },
            ],
          });
        }
      },
      onPlayerWillPrepare(player: TTVideoEngine) {
        console.log('player will prepare', player);
      },
      onPlayerExtraSetup(player: TTVideoEngine, source: VideoSource) {
        console.log('player extra setup', player, source);
      },
    });
  }, []);

  const onScrollBeginDrag = useCallback(() => {
    setScrollDrag(true);
  }, []);
  const onScrollEndDrag = useCallback(() => {
    setScrollDrag(false);
  }, []);

  return (
    <SafeAreaView style={styles.wrapper}>
      <Carousel
        style={{width: '100%', height: '100%'}}
        vertical
        afterChange={onIndexChanged}
        onScrollBeginDrag={onScrollBeginDrag}
        onScrollEndDrag={onScrollEndDrag}
        overScrollMode="never">
        {sourceDataList.map((item, index) => {
          return (
            <View key={item.vid}>
              <PrePlayer
                isScrollDrag={isScrollDrag}
                data={item}
                currentIndex={currentIndex}
                index={index}
              />
            </View>
          );
        })}
      </Carousel>
    </SafeAreaView>
  );
};

export default PreRender;
```


Below is an example code that implements pre\-rendering using the React Native playback view component:

```TypeScript
// PrePlayer.tsx
import React, {useCallback, useEffect, useMemo, useRef, useState} from 'react';
import {View, StyleSheet, Image} from 'react-native';
import {
  PlayerViewComponent,
  TTVideoEngine,
  VideoSource,
  createDirectUrlSource,
  getPreRenderEngine,
  setView,
  initPlayer,
  getFirstFrameEngine,
  type DirectUrlSourceInitProps,
} from '@byteplus/react-native-vod-player';

interface SwiperPlayerProps {
  currentIndex: number;
  index: number;
  data: DirectUrlSourceInitProps & {
    poster: string;
  };
  isScrollDrag: boolean;
}

const styles = StyleSheet.create({
  wrap: {
    position: 'relative',
    width: '100%',
    height: '100%',
  },
  player: {
    width: '100%',
    height: '100%',
    backgroundColor: '#000000',
  },
  img: {
    position: 'absolute',
    width: '100%',
    height: '100%',
    resizeMode: 'contain',
    top: 0,
    left: 0,
    backgroundColor: '#000000',
  },
});

const PrePlayer: React.FC<SwiperPlayerProps> = ({
  currentIndex,
  index,
  data,
  isScrollDrag,
}) => {
  const isCurrent = useMemo(
    () => index === currentIndex,
    [index, currentIndex],
  );
  const viewId = useMemo<string>(() => `pre-player-${index}`, [index]);
  const [canInit, setCanInit] = useState(false);
  // Pre-rendering engine
  const playerRef = useRef<TTVideoEngine | undefined>();
  const [showPoster, setShowPoster] = useState(true);

  const handleStart = useCallback(() => {
    setCanInit(true);
  }, []);

  const setPlayer = useCallback(async () => {
    if (!playerRef.current) {
      setShowPoster(true);
      const curSource: VideoSource = createDirectUrlSource(data);
      const preRenderEngine = getPreRenderEngine(curSource);
      if (preRenderEngine && index !== 0) {
        // Pre-rendering is successful
        await setView(preRenderEngine, viewId);
        setShowPoster(false);
        playerRef.current = preRenderEngine;
      } else {
        // Pre-rendering is failed
        const player = await initPlayer({viewId});
        player.setVideoSource(curSource);
        playerRef.current = player;
        playerRef.current?.setListener({
          onReadyToDisplay() {
            setShowPoster(false);
          },
        });
      }
      if (isCurrent) {
        playerRef.current?.play();
      }
    }
  }, [data, index, isCurrent, viewId]);

  useEffect(() => {
    return () => {
      playerRef.current?.close();
    };
  }, []);

  useEffect(() => {
    if (!isCurrent) {
      playerRef.current?.close();
      playerRef.current = undefined;
      setShowPoster(true);
    } else {
      if (canInit) {
        setPlayer();
      }
    }
  }, [canInit, index, isCurrent, setPlayer]);

  const whenDrag = useCallback(async () => {
    if (canInit) {
      const source: VideoSource = createDirectUrlSource(data);
      const preRenderEngine = getFirstFrameEngine(source);
      if (preRenderEngine) {
        console.log('hit prerender, set first frame');
        await setView(preRenderEngine, viewId);
      }
    }
  }, [canInit, data, viewId]);

  useEffect(() => {
    if (index === currentIndex + 1 && isScrollDrag) {
     // Use the pre-rendering instance to set the first frame of the video as the cover for the next view.
      whenDrag();
    }
  }, [canInit, currentIndex, index, isCurrent, isScrollDrag, whenDrag]);

  return (
    <View style={styles.wrap}>
      <PlayerViewComponent
        style={styles.player}
        viewId={viewId}
        onLoad={handleStart}
      />
      <Image
        style={[styles.img, showPoster ? {opacity: 1} : {opacity: 0}]}
        source={{uri: data.poster}}
      />
    </View>
  );
};

export default PrePlayer;
```
