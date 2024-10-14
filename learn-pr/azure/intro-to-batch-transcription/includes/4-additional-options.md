Azure batch transcription isn't only a replacement for manual transcription. It's a robust transcription service that, with a little creativity, can solve various business problems.

In our scenario, your call center has come across challenges with the audio data, such as background noise, language, and dialect barriers. Overall, these issues make human-led transcription challenging, time-consuming, and prone to errors. These errors can lead to compliance issues or can compound customer problems when unresolved requests aren't properly flagged. What's more, you notice that staff retention is low as a result of tense customer interactions. You want to remedy this situation so that your staff knows they're supported in their roles.

## Customizing your solution

You've been wondering if there's a way batch transcription can help you mitigate these specific problems that your office and staff are facing. While standard batch transcription doesn't seem to deal with these particular problems, creating a Custom model might be the solution you need.

### Language and dialect barriers

One of the main problems your office handles is the wide variety of languages and dialects, because your call-center organization manages calls from all over the world. Because of this global reach, transcription requires experienced speakers of each language. Even then, transcription leads to some misunderstandings given the accents and dialects from each region. Calls from the United States or Spain can be in various languages, while Australian calls can contain colorful local slang that can baffle native speakers from the Northern Hemisphere.

Locale-aware batch transcription can be used to transcribe audio data from different sources, taking into account not just language, but dialects and local pronunciations.

### Custom models

Audio analysis often looks for specific phrases or words, such as requests for particular actions to be undertaken, or for product names. Analysis can be complicated when servicing many areas of the globe. For example, your call center might be responsible for products or services that differ by region and that use brand names that can't be found in the dictionary and are easily misheard. There can also be different regulatory requirements for each region you're servicing and a need to identify different phrases with high degrees of accuracy.

When the number of important specific phrases grows beyond a few hundred words, you might prefer to customize batch transcription more extensively by building a *Custom Speech model*. This type of model is something we explore in the next set of exercises. In short, custom speech lets you evaluate and improve transcription accuracy for your applications and products by training and testing a model using your own audio files. Custom speech can help you overcome speech recognition barriers, such as industry-specific terminology or unusual background noise, to provide accurate audio transcription.

A custom speech model can be made by using the custom speech tool in the Speech Studio, which is a customization portal for Azure Speech Service. You're provided with instructions each step of the way within the portal. By providing audio with human-labeled transcripts, related texts, and pronunciation guidance, you're able to deploy your own custom model.

In our scenario, a custom model helps you overcome the problems your office is facing with background noise and accents, because custom models are trained specifically to your environment. You also see that custom models can be trained to your industry-specific vocabulary and the proper pronunciation of your key terms.

## Analyzing data deeper

Converting speech to text using batch transcription offers more business opportunities using Azure services. For example, the JSON format produced by batch transcription is readily indexable, and is digestible by services such as the *Text Analytics Sentiment Analysis or Opinion Mining* service. This service can identify the aspects of the conversation the speaker felt positively or negatively about, which lets you get further insights from your data to take actions leading to more positive outcomes.

![Diagram showing Text Analytics sentiment analysis versus opinion mining.](../media/4-text-analytics-example.png)
