---
slug: debugging-web-pages-on-the-nokia-8110-with-kaios
date: 2019-03-21T21:41:53.555Z
title: 'Debugging Web Pages on the Nokia 8110 with KaiOS'
link: ''
tags: [links, kaios, debugging, firefox]
---
ఇటీవల మేము ఫీచర్ ఫోన్లలో చాలా అభివృద్ధి చేస్తున్నాం మరియు ఇది చాలా కష్టం, కానీ సరదాగా ఉంది. కయోస్ లో మేము వెబ్ పేజీలను డీబగ్ చేయలేకపోయాము, ముఖ్యంగా మేము కలిగి ఉన్న హార్డువేరులో (ది నోకియా 8110) డబ్బింగ్ చేయలేకపోయాము. నోకియా ఒక గొప్ప పరికరం, అది మనకు తెలిసిన కైస్ తో నిర్మించబడింది, ఇది ఫైర్ఫాక్స్ 48 కి సమానంగా ఉంటుంది, కానీ ఇది లాక్ చేయబడింది, మీకు ఇతర Android పరికరాల్లో లభించే సంప్రదాయ డెవలపర్ మోడ్ లేదు, WebIDE సులభంగా.

కొన్ని బ్లాగ్లను చదివిన కలయికతో మరియు `adb` గురించి ఒక బిట్ తెలుసుకోవడం `adb` నేను దీన్ని ఎలా చేయాలో పని `adb` . గమనిక, ఇతరులు దీన్ని చేయగలిగారు, కానీ ఇది ఒకే స్థలంలో స్పష్టంగా నమోదు చేయబడలేదు.

<figure>
  <img src="/images/2019-03-21-debugging-web-pages-on-the-nokia-8110-with-kaios.jpeg">
</figure>

(పైన ఉన్న చిత్రం DevTools మరియు స్క్రీన్షాట్ సాధనం యొక్క అవుట్పుట్ను చూపుతుంది)

ఇక్కడ దశలు ఉన్నాయి:

1. USB కేబుల్ను కనెక్ట్ చేయండి. మీరు మీ ప్రధాన మెషీన్లో `adb` ఇన్స్టాల్ చేసుకున్నారని నిర్ధారించుకోండి.
2. [Firefox 48](https://archive.mozilla.org/pub/firefox/releases/48.0.2/) యొక్క కాపీని డౌన్ లోడ్ [Firefox 48](https://archive.mozilla.org/pub/firefox/releases/48.0.2/) (ఇది నేను పని చేయగల [Firefox 48](https://archive.mozilla.org/pub/firefox/releases/48.0.2/) )
3. మీ ఫోన్ నుండి `*#*#33284#*#*` లోకి ప్రవేశించడం ద్వారా &#39;డెవలపర్ మోడ్&#39; ను ఎనేబుల్ చేయండి (గమనిక, డయలర్ను ఉపయోగించవద్దు). మీరు తెరపై ఉన్న చిన్న &#39;బగ్&#39; చిహ్నాన్ని చూస్తారు. [[Source](https://groups.google.com/forum/#!topic/bananahackers/MIpcrSXTRBk) ]
4. మీ USB కేబుల్ను అటాచ్ చేయండి
5. మీ డెవలప్మెంట్ మెషీన్లో కింది ఆదేశాలను అమలు చేయండి
1. `adb start-server`
2. మీ ఫోన్ను తనిఖీ చేయడానికి `adb devices` కనెక్ట్ చేయబడింది.
3. `adb forward tcp:6000 localfilesystem:/data/local/debugger-socket` ఇది మీ మెషీన్ నుండి ఒక ఛానెల్ను ఫోన్లో ఒక సాకెట్కు సెటప్ చేస్తుంది. ఇది వెబ్ IDE ఉపయోగిస్తుంది.
6. ఫైర్ఫాక్స్ ప్రారంభించడం ద్వారా `Web IDE` ను ప్రారంభించండి, ఉపకరణాలు మరియు వెబ్ IDE కి వెళ్ళండి
7. వెబ్ IDE ఓపెన్ అవుతుంది, &#39;రిమోట్ రన్టైమ్&#39; క్లిక్ చేసి, &#39;localhost: 6000&#39; (ఓపెన్ బటన్) ను క్లిక్ చేయండి (ఇది tcp ఫార్వార్డింగ్ పోర్ట్).
8. ఫోన్లో ఒక పేజీ తెరవండి, మరియు మీరు దానిని ఎడమవైపు చూడాలి. Voila.
