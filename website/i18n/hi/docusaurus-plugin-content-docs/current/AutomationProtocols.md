---
id: automationProtocols
title: स्वचालन प्रोटोकॉल
---

WebdriverIO के साथ, आप अपने E2E परीक्षणों को स्थानीय रूप से या क्लाउड में चलाते समय कई स्वचालन तकनीकों के बीच चयन कर सकते हैं। डिफ़ॉल्ट रूप से WebdriverIO हमेशा ऐसे ब्राउज़र ड्राइवर की जाँच करेगा जो `localhost:4444`पर WebDriver प्रोटोकॉल के अनुरूप हो। यदि उसे ऐसा ड्राइवर नहीं मिलता है तो वह हुड के नीचे पपेटियर का उपयोग करके Chrome DevTools का उपयोग करने के लिए जाता है।

लगभग सभी आधुनिक ब्राउज़र जो [WebDriver](https://w3c.github.io/webdriver/) का समर्थन करते हैं, [DevTools](https://chromedevtools.github.io/devtools-protocol/) नामक एक अन्य मूल इंटरफ़ेस का भी समर्थन करते हैं जिसका उपयोग स्वचालन उद्देश्यों के लिए किया जा सकता है।

आपके उपयोग के मामले और पर्यावरण के आधार पर दोनों के फायदे और नुकसान हैं।

## वेबड्राइवर प्रोटोकॉल

> [वेबड्राइवर](https://w3c.github.io/webdriver/) एक रिमोट कंट्रोल इंटरफ़ेस है जो उपयोगकर्ता एजेंटों के इंट्रोस्पेक्सन और नियंत्रण को सक्षम बनाता है। यह वेब ब्राउज़र के व्यवहार को दूर से निर्देश देने के लिए आउट-ऑफ़-प्रोसेस प्रोग्राम के लिए एक प्लेटफ़ॉर्म- और भाषा-तटस्थ वायर प्रोटोकॉल प्रदान करता है।

वेबड्राइवर प्रोटोकॉल को उपयोगकर्ता के दृष्टिकोण से एक ब्राउज़र को स्वचालित करने के लिए डिज़ाइन किया गया था, जिसका अर्थ है कि एक उपयोगकर्ता जो कुछ भी करने में सक्षम है, आप ब्राउज़र के साथ कर सकते हैं। यह कमांड का एक सेट प्रदान करता है जो किसी एप्लिकेशन के साथ सामान्य इंटरैक्शन को दूर करता है (उदाहरण के लिए, किसी तत्व की स्थिति को नेविगेट करना, क्लिक करना या पढ़ना)। चूंकि यह एक वेब मानक है, यह सभी प्रमुख ब्राउज़र विक्रेताओं में अच्छी तरह से समर्थित है, और इसका उपयोग [एपियम](http://appium.io)का उपयोग करके मोबाइल स्वचालन के लिए अंतर्निहित प्रोटोकॉल के रूप में भी किया जा रहा है।

इस ऑटोमेशन प्रोटोकॉल का उपयोग करने के लिए, आपको एक प्रॉक्सी सर्वर की आवश्यकता होती है जो सभी आदेशों का अनुवाद करता है और उन्हें लक्षित वातावरण (यानी ब्राउज़र या मोबाइल ऐप) में निष्पादित करता है।

ब्राउज़र ऑटोमेशन के लिए, प्रॉक्सी सर्वर आमतौर पर ब्राउज़र ड्राइवर होता है। सभी ब्राउज़रों के लिए ड्राइवर उपलब्ध हैं:

- Chrome – [ChromeDriver](http://chromedriver.chromium.org/downloads)
- Firefox – [Geckodriver](https://github.com/mozilla/geckodriver/releases)
- Microsoft Edge – [Edge Driver](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)
- Internet Explorer – [InternetExplorerDriver](https://github.com/SeleniumHQ/selenium/wiki/InternetExplorerDriver)
- Safari – [SafariDriver](https://developer.apple.com/documentation/webkit/testing_with_webdriver_in_safari)

किसी भी तरह के मोबाइल ऑटोमेशन के लिए, आपको [एपियम](http://appium.io)को इंस्टॉल और सेटअप करना होगा। यह आपको उसी वेबड्राइवरआईओ सेटअप का उपयोग करके मोबाइल (आईओएस/एंड्रॉइड) या यहां तक कि डेस्कटॉप (मैकओएस/विंडोज) अनुप्रयोगों को स्वचालित करने की अनुमति देगा।

ऐसी बहुत सी सेवाएँ भी हैं जो आपको उच्च स्तर पर क्लाउड में अपना स्वचालन परीक्षण चलाने की अनुमति देती हैं। इन सभी ड्राइवरों को स्थानीय रूप से सेटअप करने के बजाय, आप क्लाउड में इन सेवाओं (जैसे [सॉस लैब्स](https://saucelabs.com)) से बात कर सकते हैं और उनके प्लेटफॉर्म पर परिणामों का निरीक्षण कर सकते हैं। परीक्षण स्क्रिप्ट और स्वचालन वातावरण के बीच संचार इस प्रकार दिखाई देगा:

![वेब ड्राइवर सेटअप](/img/webdriver.png)

### लाभ

- आधिकारिक W3C वेब मानक, सभी प्रमुख ब्राउज़रों द्वारा समर्थित
- सरलीकृत प्रोटोकॉल जो सामान्य उपयोगकर्ता इंटरैक्शन को कवर करता है
- मोबाइल स्वचालन के लिए समर्थन (और यहां तक कि देशी डेस्कटॉप ऐप्स)
- [सॉस लैब्स](https://saucelabs.com)जैसी सेवाओं के माध्यम से स्थानीय और साथ ही क्लाउड में उपयोग किया जा सकता है

### नुकसान

- गहन ब्राउज़र विश्लेषण के लिए डिज़ाइन नहीं किया गया है (उदाहरण के लिए, नेटवर्क ईवेंट का पता लगाना या इंटरसेप्ट करना)
- स्वचालन क्षमताओं का सीमित सेट (उदाहरण के लिए, सीपीयू या नेटवर्क को थ्रॉटल करने के लिए कोई समर्थन नहीं)
- ब्राउज़र ड्राइवर को सेलेनियम-स्टैंडअलोन/क्रोमड्राइवर/आदि के साथ सेट करने के लिए अतिरिक्त प्रयास
