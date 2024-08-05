<div align="center">

[<img src="readme_files/logo.png" alt="gradio" width=400>](https://gradio.app)<br>

<span style="color: grey; font-weight: 300; font-family: 'Chalkboard', sans-serif;" >Easy and affordable APIs for AI models</span>

[Website](https://ai.voilatech.co.jp/)
| [API Docs](https://ai.voilatech.co.jp/Docs/)
| [Guides](https://ai.voilatech.co.jp/guides/)
| [Pricing](https://ai.voilatech.co.jp/guides/models-and-pricing)

</div>

### What is this
Tired of CUDA errors, long installation times, and expensive cloud services? VoilaTech AI APIs offers easy-to-use APIs for popular open-source AI models with a simple, affordable pricing.

We currently offer a Speech-to-Text API and a vocal / background music separation API from USD$0.04 per hour of audio.

<details>
    <summary>Speech-to-Text Transcription or Alignment</summary>
Speech-to-Text API is powered by <a href="https://github.com/SYSTRAN/faster-whisper">Faster-Whisper</a> with the <a href="https://github.com/jianfch/stable-ts">Stable-ts</a> implementation. It provides word-level transcriptions of audio files. Models ranges from tiny to large, with the new distil model and a fined-tuned model for Japanese.

Two tasks are available: transcribe and align. Transcribe provides provides the text transcription along with word-level timestamps given the audio. Align provides the word-level timestamps given the audio and the text. Use align if you have the non-timed text and want to get the timestamps, as it is more accurate and cheaper.
</details>

<details>
    <summary>Vocal / Background Music Separation API</summary>
Vocal / Background Music Separation API is powered by <a href="https://github.com/adefossez/demucs">Demucs</a>. It provides separated audio files of the vocals, drums, bass, and other instruments in an audio/music file. Currently only the hybrid htdemucs model is available.
</details>

### Get Started

1. Head over to our [website](https://ai.voilatech.co.jp/) and sign up for an account.

2. Generate an API key from in [Account](https://bideogo.voilatech.co.jp/setting) > API Key Management.

3. Use this key to call the Whisper model to obtain word-level transcriptions of your audio files.

<details>
    <summary>Javascript Example</summary>

```javascript
const request = require('request');

const options = {
  method: 'POST',
  url: 'https://api.voilatech.co.jp/v1/stablets/transcribe',
  headers: {'Content-Type': 'application/json', 'Api-Key': 'YOUR_TOKEN'},
  body: {
    model: 'large-v2',
    audio_url: 'https://longstoragevoila.blob.core.windows.net/long/zaiye.mp3'
  },
  json: true
};

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```
</details>

<details>
    <summary>Python Example</summary>
    
```python
import requests

response = requests.post('https://ytdlp-voilatech-apim.azure-api.net/v1/stablets/transcribe', json={
    'model': 'large-v2',
    'audio_url': 'https://longstoragevoila.blob.core.windows.net/long/zaiye.mp3'
}, headers={
    'Api-Key': 'YOUR_TOKEN'
})

print(response.json())
```
</details>

4. Because AI models can be running for some time, we will return a job ID that you can use to check the 
status of the job. You can use the job ID to check the status of the job and get the results when it is done.

<details>
    <summary>Javascript Example</summary>

```javascript
const request = require('request');

const options = {
  method: 'GET',
  url: 'https://api.voilatech.co.jp/v1/demucs/status',
  qs: {id: ''},
  headers: {'Api-Key': 'YOUR_TOKEN'}
};

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```
</details>

<details>
    <summary>Python Example</summary>
    
```python
import requests

url = "https://ytdlp-voilatech-apim.azure-api.net/v1/stablets/status"

querystring = {"id":""}

headers = {"Api-Key": "YOUR_TOKEN"}

response = requests.get(url, headers=headers, params=querystring)

print(response.json())
```
</details>


5. Done! You now have the ability to use AI models anywhere, anytime, with any programming language.


### Frequently Asked Questions

<details>
  <summary>What service do you provide?</summary>
  <p>We offer easy-to-use API service for popular open-source AI models with a simple, affordable pricing. </p>
</details>

<details>
  <summary>Why should I use your service instead of using the open-source model directly?</summary>
  <p>Yes, of course you can use the open-source model directly if you follow the instructions on huggingface and github. However, many models require some machine-learning coding knowledge in python and some effort to get them working. Also, there is no clear way of how to use them in production, such as in a mobile app. With VoilaTech AI APIs, you can get levearge AI abilities consistantly from familiar open-source models on any device using any programming language.</p>
</details>


<details>
  <summary>Why should I use your Whisper API instead of using OpenAI's API?</summary>
  <p>Because we use the equivalent model at better price. In addition, we offer alternative models that is cheaper or fine-tined for certain tasks. We also use the stable-ts library to achieve more accurate timestamps.</p>
</details>

<details>
  <summary>Do I pay if I am not using the service?</summary>
  <p>No, you are charged only if you make a request.</p>
</details>

<details>
  <summary>Will I pay for failed requests?</summary>
  <p>Yes, but please let me explain. We let you tweak all the advanced features and choose your model like you would on your own machine. This has the benefit of allowing you to have full control of your AI's behavior. However, this also means that under certain circumstances, you may make requests that are not optimal and may not return the expected results, or even errors. Therefore, you will be charged for all requests made to the server. However, we do offer some free credits to get you started, and we also plan to released a pay-only-if-success version in the future.</p>
</details>

<details>
  <summary>How will I be billed?</summary>
  <p>You would need to top up with a minimum of USD$5 to be able to use our service. Your credit will expire in a year. For your requests, you will be charged to the nearest second.</p>
</details>


<details>
  <summary>Can I choose my own model?</summary>
  <p>Yes, we try to offer a wide selection of models for each task and is explicity about the models that we use. Therefore, you may be able to choose a smaller model to save cost while obtaining consistant results.</p>
</details>

<details>
  <summary>Why are your prices so low? Is your service reliable?</summary>
  <p>We are a small team based in Japan. We take advantage of the cheap living-cost here to keep the prices low. However, our services is very reliable as we use production-ready technologies supplied by big tech companies.</p>
</details>

<details>
  <summary>Can I use your service in production?</summary>
  <p>Yes. Our services is very reliable and optimized for production. We use production-ready technologies supplied by big tech companies.</p>
</details>


<small>*This repository is used to report issues, request features, and discuss the VoilaTech AI APIs. If you have any questions, feel free to open an issue.*</small>