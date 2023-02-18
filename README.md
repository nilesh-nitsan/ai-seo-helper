# TYPO3 Extension `AI SEO Helper`

Generates SEO metadata based on page content using AI. Currently, both the meta description and the keywords can be generated using an additional button next to the corresponding text fields.

## Installation

Add via composer:

    composer require "passionweb/ai-seo-helper"

* Install the extension via composer
* Flush TYPO3 and PHP Cache

## Requirements

You need an OpenAI account and API key. If you have not yet created an account or key, you can do so using the following links.

Source: [Create OpenAI account](https://platform.openai.com/signup "Create OpenAI account")

Source: [Create API key](https://platform.openai.com/account/api-keys "Create API key")

## Generate meta description

Added an additional button <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" xml:space="preserve" viewBox="0 0 16 16"><g class="icon-color"><path d="M6.768 15H1.5a.5.5 0 0 1-.5-.5v-13a.5.5 0 0 1 .5-.5h13a.5.5 0 0 1 .5.5v5.47a5.779 5.779 0 0 0-1-.831V2H2v12h3.975c.227.362.493.698.793 1Zm-1.572-3H3v1h2.476a5.707 5.707 0 0 1-.28-1Zm-.018-2H3v1h2.1a5.87 5.87 0 0 1 .078-1Zm.735-2H3v1h2.44c.125-.35.285-.685.473-1Zm2.01-2H3v1h3.671a5.775 5.775 0 0 1 1.251-1ZM3 3h10v2H3V3Zm8 9a1 1 0 1 0 0-2 1 1 0 0 0 0 2ZM9.285 8.55l-.517-.86a4 4 0 0 1 6.248 3.307h.825c.14 0 .226.161.151.285l-1.307 2.433a.175.175 0 0 1-.304 0l-1.357-2.433c-.075-.124.011-.284.151-.284h.84a3 3 0 0 0-4.73-2.449ZM11.024 14c.645 0 1.218-.203 1.707-.55l.517.86A4 4 0 0 1 7 11.002h-.817c-.14 0-.226-.161-.152-.285l1.3-2.433a.175.175 0 0 1 .304 0l1.316 2.433c.074.124-.012.284-.152.284H8C8.001 12.658 9.368 14 11.024 14Z"/></g></svg> next to the meta description text field. When you click this button, the (text) content of the selected page is generated and a meta description that is as suitable as possible is created with the help of the AI. Currently, the page must not be deactivated in the backend. Depending on the page size, the process may take a few seconds. However, notifications are used to display appropriate information.

![Generate meta description](./Documentation/Editor/generate-meta-description.png)

It can happen that the AI ​​returns texts that exceed the maximum allowed length of the meta description. To additionally check the length of the meta description, the extension ["Yoast SEO for TYPO3"](https://extensions.typo3.org/extension/yoast_seo "Yoast SEO for TYPO3") can be used, for example, or various online tools.

## Generate keywords

Added an additional button <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" xml:space="preserve" viewBox="0 0 16 16"><g class="icon-color"><path d="M6.768 15H1.5a.5.5 0 0 1-.5-.5v-13a.5.5 0 0 1 .5-.5h13a.5.5 0 0 1 .5.5v5.47a5.779 5.779 0 0 0-1-.831V2H2v12h3.975c.227.362.493.698.793 1Zm-1.572-3H3v1h2.476a5.707 5.707 0 0 1-.28-1Zm-.018-2H3v1h2.1a5.87 5.87 0 0 1 .078-1Zm.735-2H3v1h2.44c.125-.35.285-.685.473-1Zm2.01-2H3v1h3.671a5.775 5.775 0 0 1 1.251-1ZM3 3h10v2H3V3Zm8 9a1 1 0 1 0 0-2 1 1 0 0 0 0 2ZM9.285 8.55l-.517-.86a4 4 0 0 1 6.248 3.307h.825c.14 0 .226.161.151.285l-1.307 2.433a.175.175 0 0 1-.304 0l-1.357-2.433c-.075-.124.011-.284.151-.284h.84a3 3 0 0 0-4.73-2.449ZM11.024 14c.645 0 1.218-.203 1.707-.55l.517.86A4 4 0 0 1 7 11.002h-.817c-.14 0-.226-.161-.152-.285l1.3-2.433a.175.175 0 0 1 .304 0l1.316 2.433c.074.124-.012.284-.152.284H8C8.001 12.658 9.368 14 11.024 14Z"/></g></svg>
next to the keywords text field. When you click this button, the (text) content of the selected page is generated and keywords that is as suitable as possible is created with the help of the AI. Currently, the page must not be deactivated in the backend. Depending on the page size, the process may take a few seconds. However, notifications are used to display appropriate information.

![Generate keywords](./Documentation/Editor/generate-keywords.png)

## Extension settings

You can adapt the following parameters to your personal needs. After the first tests, the best results were achieved with the predefined values. However, this is no guarantee that these values ​​will also achieve the best results for you.

### `openAiApiKey`

    # cat=basic; type=string; label=OpenAI Secret Key
    openAiApiKey = YOUR_API_KEY

Enter your generated API key.

### `openAiPromptPrefixMetaDescription`

    # cat=basic; type=string; label=Prompt-Prefix for meta description generation
    openAiPromptPrefixMetaDescription = Extract seo meta description in one short sentence and with a maximum of 150 characters or less for following text

Enter your instruction for generating meta description. Since OpenAI calculates the length of the content with tokens (an explanation of the conversion of tokens into characters and sentences can be found [here](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them#:~:text=Tokens%20can%20be%20thought%20of,spaces%20and%20even%20sub%2Dwords. "")) by default, we have to explicitly tell the AI ​​the desired total length and the type of expected creation

### `replaceTextMetaDescription`

    # cat=basic; type=string; label=Replace first part of generated meta description content
    replaceTextMetaDescription = Meta Description:

The content generated by OpenAI is usually supplemented with a short introduction. Here you can define the part of the generated content that should be removed.

### `openAiPromptPrefixKeywords`

    # cat=basic; type=string; label=Prompt-Prefix for keywords generation
    openAiPromptPrefixKeywords = Extract seo keywords from this text

Enter your instruction for generating keywords.

### `replaceTextKeywords`

    # cat=basic; type=string; label=Replace first part of generated keywords
    replaceTextKeywords = SEO keywords:

The content generated by OpenAI is usually supplemented with a short introduction. Here you can define the part of the generated content that should be removed.

### `openAiModel`

    # cat=basic; type=string; label=OpenAI Model
    openAiModel = text-davinci-003

The id of the model which will generate the completion. See [models overview](https://platform.openai.com/docs/models/overview "models overview") for an overview of available models.

### `openAiTemperature`

    # cat=basic; type=double+; label=OpenAI Temperature
    openAiTemperature = 0.5

What sampling temperature to use, between 0 and 2. Higher values like 0.8 will make the output more random, while lower values like 0.2 will make it more focused and deterministic.

### `openAiMaxTokens`

    # cat=basic; type=int+; label=OpenAI Max-Tokens
    openAiMaxTokens = 175

The token ([what are tokens and how to count them](https://help.openai.com/en/articles/4936856-what-are-tokens-and-how-to-count-them#:~:text=Tokens%20can%20be%20thought%20of,spaces%20and%20even%20sub%2Dwords. "")) count of your prompt plus max_tokens cannot exceed the model's context length. Most models have a context length of 2048 tokens (except for the newest models, which support 4096).

### `openAiTopP`

    # cat=basic; type=int+; label=OpenAI Top-P
    openAiTopP = 1

An alternative to sampling with temperature, called nucleus sampling, where the model considers the results of the tokens with top_p probability mass. So 0.1 means only the tokens comprising the top 10% probability mass are considered.

### `openAiFrequencyPenalty`

    # cat=basic; type=double; label=OpenAI Frequency Penalty
    openAiFrequencyPenalty = 0.8

Number between -2.0 and 2.0. Positive values penalize new tokens based on their existing frequency in the text so far, decreasing the model's likelihood to repeat the same line verbatim.

### `openAiPresencePenalty`

    # cat=basic; type=double; label=OpenAI Presence Penalty
    openAiPresencePenalty = 0

Number between -2.0 and 2.0. Positive values penalize new tokens based on whether they appear in the text so far, increasing the model's likelihood to talk about new topics.

## Troubleshooting and logging

If something does not work as expected take a look at the log file first.
Every problem is logged to the TYPO3 log (normally found in `var/log/typo3_*.log`)

## Notices to keep in mind

Just like this extension, OpenAI is still in development mode and not fully mature. For this reason, we urgently advise you to check all generated texts for correctness before saving them and to make any necessary adjustments!

## Achieving more together or Feedback, Feedback, Feedback

I'm grateful for any feedback! Be it suggestions for improvement, extension requests or just a (constructive) feedback on how good or crappy the extension is.

Feel free to send me your feedback to [service@passionweb.de](mailto:service@passionweb.de "Send Feedback") or [contact me on Slack](https://typo3.slack.com/team/U02FG49J4TG "Contact me on Slack")
