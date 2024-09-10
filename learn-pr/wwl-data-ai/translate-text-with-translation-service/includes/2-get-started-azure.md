Microsoft provides Azure AI services that support translation. Specifically, you can use the following services:

- The **Azure AI Translator** service, which supports text-to-text translation.
- The **Azure AI Speech** service, which enables speech to text and speech-to-speech translation.

## Azure resources for Azure AI Translator and Azure AI Speech

Before you can use Azure AI Translator or Azure AI Speech, you must provision appropriate resources in your Azure subscription.

There are dedicated **Translator** and **Speech** resource types for these services, which you can use if you want to manage access and billing for each service individually.

Alternatively, you can create an **Azure AI services** resource that provides access to both services through a single Azure resource, consolidating billing and enabling applications to access both services through a single endpoint and authentication key.

## Text translation with Azure AI Translator

Azure AI Translator is easy to integrate in your applications, websites, tools, and solutions. The service uses a Neural Machine Translation (NMT) model for translation, which analyzes the semantic context of the text and renders a more accurate and complete translation as a result.

### Azure AI Translator language support

Azure AI Translator supports text-to-text translation between [more than 60 languages](/azure/ai-services/Translator/language-support?azure-portal=true). When using the service, you must specify the language you are translating ***from*** and the language you are translating ***to*** using ISO 639-1 language codes, such as *en* for English, *fr* for French, and *zh* for Chinese. Alternatively, you can specify cultural variants of languages by extending the language code with the appropriate 3166-1 cultural code - for example, *en-US* for US English, *en-GB* for British English, or *fr-CA* for Canadian French.

When using Azure AI Translator, you can specify one ***from*** language with multiple ***to*** languages, enabling you to simultaneously translate a source document into multiple languages.

### Optional Configurations

Azure AI Translator's application programming interface (API) offers some optional configuration to help you fine-tune the results that are returned, including:

- **Profanity filtering**.  Without any configuration, the service will translate the input text, without filtering out profanity. Profanity levels are typically culture-specific but you can control profanity translation by either marking the translated text as profane or by omitting it in the results.
- **Selective translation**. You can tag content so that it isn't translated. For example, you may want to tag code, a brand name, or a word/phrase that doesn't make sense when localized.

## Speech translation with Azure AI Speech

Azure AI Speech includes the following APIs:

- **Speech to text** - used to transcribe speech from an audio source to text format.
- **Text to speech** - used to generate spoken audio from a text source.
- **Speech Translation** - used to translate speech in one language to text or speech in another.

You can use the **Speech Translation** API to translate spoken audio from a streaming source, such as a microphone or audio file, and return the translation as text or an audio stream. This enables scenarios such as real-time closed captioning for a speech or simultaneous two-way translation of a spoken conversation.

### Azure AI Speech language support 

As with Azure AI Translator, you can specify one source language and one or more target languages to which the source should be translated with Azure AI Speech. You can translate speech into [over 60 languages](/azure/ai-services/speech-service/language-support?tabs=stt#speech-translation?azure-portal=true).

The source language must be specified using the extended language and culture code format, such as *es-US* for American Spanish. This requirement helps ensure that the source is understood properly, allowing for localized pronunciation and linguistic idioms.

The target languages must be specified using a two-character language code, such as *en* for English or *de* for German.
