---
title: Languages
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
![](https://files.readme.io/ee442e3-image.png)

## Supported Languages

With Botpress, you can build chatbots that are able to converse with people in more than 100+ languages!

|                                      |                      |                    |                     |                  |
| :----------------------------------- | :------------------- | :----------------- | :------------------ | :--------------- |
| Afrikaans                            | Albanian             | Alemannic          | Amharic             | Arabic           |
| Aragonese                            | Armenian             | Assamese           | Asturian            | Azerbaijani      |
| Bashkir                              | Basque               | Bavarian           | Belarusian          | Bengali          |
| Bihari                               | Bishnupriya Manipuri | Bosnian            | Breton              | Bulgarian        |
| Burmese                              | Catalan              | Cebuano            | Central Bicolano    | Chechen          |
| Chinese (Simplified and Traditional) | Chuvash              | Corsican           | Croatian            | Czech            |
| Danish                               | Divehi               | Dutch              | Eastern Punjabi     | Egyptian Arabic  |
| Emilian-Romagnol                     | Erzya                | Esperanto          | Estonian            | Fiji Hindi       |
| Finnish                              | French               | Galician           | Georgian            | German           |
| Goan Konkani                         | Greek                | Gujarati           | Haitian             | Hebrew           |
| Hill Mari                            | Hindi                | Hungarian          | Icelandic           | Ido              |
| Ilokano                              | Indonesian           | Interlingua        | Irish               | Italian          |
| Japanese                             | Javanese             | Kannada            | Kapampangan         | Kazakh           |
| Khmer                                | Kirghiz              | Korean             | Kurdish (Kurmanji)  | Kurdish (Sorani) |
| Latin                                | Latvian              | Limburgish         | Lithuanian          | Lombard          |
| Low Saxon                            | Luxembourgish        | Macedonian         | Maithili            | Malagasy         |
| Malay                                | Malayalam            | Maltese            | Manx                | Marathi          |
| Mazandarani                          | Meadow Mari          | Minangkabau        | Mingrelian          | Mongolian        |
| Mangolian                            | Nahautl              | Neapolitan         | Nepali              | Newar            |
| North Frisian                        | Northern Sotho       | Norwegian (Bokmål) | Norwegian (Nynorsk) | Occitan          |
| Oriya                                | Ossetian             | Palatinate German  | Pashto              | Persian          |
| Piedmontese                          | Polish               | Portuguese         | Quechua             | Romanian         |
| Romansh                              | Russian              | Sakha              | Sanskrit            | Sardinian        |
| Scots                                | Scottish Gaelic      | Serbian            | Serbo-Croatian      | Sicilian         |
| Sindhi                               | Sinhalese            | Slovak             | Slovenian           | Somali           |
| Southern Azerbaijani                 | Spanish              | Sundanese          | Swahili             | Swedish          |
| Tagalog                              | Tajik                | Tamil              | Tatar               | Telugu           |
| Thai                                 | Tibetan              | Turkish            | Turkmen             | Ukrainian        |
| Upper Sorbian                        | Urdu                 | Uyghur             | Uzbek               | Venetian         |
| Vietnamese                           | Volapük              | Walloon            | Waray               | Welsh            |
| West Flemish                         | West Frisian         | Western Punjabi    | Yiddish             | Yoruba           |
| Zazaki                               | Zeelandic            |                    |                     |                  |

<br />

## Translator Agent

[block:embed]
{
  "html": "<iframe class=\"embedly-embed\" src=\"//cdn.embedly.com/widgets/media.html?src=https%3A%2F%2Fwww.youtube.com%2Fembed%2FSIrmuihqNhs%3Ffeature%3Doembed&display_name=YouTube&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DSIrmuihqNhs&image=https%3A%2F%2Fi.ytimg.com%2Fvi%2FSIrmuihqNhs%2Fhqdefault.jpg&key=7788cb384c9f4d5dbbdbeffd9fe4b92f&type=text%2Fhtml&schema=youtube\" width=\"854\" height=\"480\" scrolling=\"no\" title=\"YouTube embed\" frameborder=\"0\" allow=\"autoplay; fullscreen; encrypted-media; picture-in-picture;\" allowfullscreen=\"true\"></iframe>",
  "url": "https://www.youtube.com/watch?v=SIrmuihqNhs",
  "title": "How to set chatbot's language in Botpress | Botpress Shorts",
  "favicon": "https://www.google.com/favicon.ico",
  "image": "https://i.ytimg.com/vi/SIrmuihqNhs/hqdefault.jpg",
  "provider": "https://www.youtube.com/",
  "href": "https://www.youtube.com/watch?v=SIrmuihqNhs",
  "typeOfEmbed": "youtube"
}
[/block]


![](https://files.readme.io/d564a21-image.png)

The Translator Agent allows your chatbot to interact with users in different languages, breaking language barriers and expanding the range of your bot's audience.

### Configuration

- **Automatically Detect User Language** - When enabled, the Translator Agent will automatically detect the user's language from their input.

Activating this feature consequently sets the `{{user.TranslatorAgent.language}}` variable when it's not already defined.

### Exposed Variables

- **user.TranslatorAgent.language**: This variable represents the detected language of the user.

### Example - setting language to french

1. Open the Toolbox Cards and drag the **Set User Language** Card into your first node(ideally).
2. Specify a language. In this case, we will use `fr` for French.

The Translator Agent automatically translates the chatbot's responses into the user's language once activated. If you wish to define the user's language manually, you can directly set the `{{user.TranslatorAgent.language}}` variable.

This variable is set to `null` by default, which means that the Translator Agent will automatically detect the user's language from their input.

### Resetting the language

Drag the **Reset User Language** Card into your flow. This will reset the `{{user.TranslatorAgent.language}}` variable to `null`.

You can do this in Execute Code card as well:

```javascript
//use null to reset the language, otherwise set it to a language code
{{user.TranslatorAgent.language}} = null;
```