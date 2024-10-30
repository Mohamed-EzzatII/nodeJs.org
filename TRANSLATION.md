Here’s a refined version of your **Node.js Website Translation Policy** that includes all the provided content, organized for clarity.

---

# Node.js Website Translation Policy

Node.js is a global platform, so this site is available in multiple languages. We use [Crowdin](https://crowdin.com) for managing translations of the Node.js Website.

The translations are handled by [Crowdin translators](https://support.crowdin.com/translation-process-overview/), and we use [`next-intl`](https://next-intl-docs.vercel.app/) as our Internationalization (i18n) library. For guidance on API usage, please see the `next-intl` documentation.

---

## How to Translate

1. Request to join the Node.js Website project on [Crowdin](https://crowdin.com/project/nodejs-web).
2. [Select the language you want to translate](https://support.crowdin.com/joining-translation-project/#starting-translation).
3. [Start translating](https://support.crowdin.com/online-editor/).

### Questions or Feedback on Translations

If you have any questions or feedback on translations, you can [start a discussion](https://crowdin.com/project/nodejs-web/discussions) by choosing "New Topic" and selecting your language from the dropdown, or open a [conversation](https://support.crowdin.com/conversations/) with the translators.

---

## Adding a New Language

To request a new language, open a discussion on the [Crowdin project](https://crowdin.com/project/nodejs-web). Once the language is added by the Crowdin manager, a Node.js Website team member can integrate it into the project.

### Steps for Adding a New Language

1. Go to `/i18n/config.json`.
2. Add the new language to the `locales` array, filling out the language object with the following fields:

   ```json
   {
     "code": "fr",
     "localName": "Français",
     "name": "French",
     "langDir": "ltr",
     "dateFormat": "DD.MM.YYYY",
     "hrefLang": "fr",
     "enabled": true
   }
   ```

| Field        | Description                                                                                        | Example       |
|--------------|----------------------------------------------------------------------------------------------------|---------------|
| `code`       | Language code (must match folder name)                                                             | `fr`          |
| `localName`  | Language name in its own language (used in language selector)                                      | `Français`    |
| `name`       | Language name in English                                                                           | `French`      |
| `langDir`    | Text direction (`ltr` for left-to-right, `rtl` for right-to-left)                                  | `ltr`         |
| `dateFormat` | Date format, following [moment.js](https://momentjs.com/docs/#/displaying/format/) conventions     | `DD.MM.YYYY`  |
| `hrefLang`   | Language code in [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) format         | `fr`          |
| `enabled`    | Specifies if the language is active                                                                | `true`        |

---

## Adding New Translation Keys

When adding translation keys for new components, follow these guidelines:

- **Add keys only in the** `i18n/locales/en.json` **file**. Crowdin will handle syncing files and notifying translators about new keys.
- **Prefix the key** based on the canonical path of the component. For example, if the component is `components/Common/MyComponent`, the prefix should be `components.common.myComponent`.
- **Use descriptive and semantic suffixes**. For instance, if a key is for “a button text that copies content to the clipboard,” the suffix could be `copyButton.title`. The final key would look like `components.common.myComponent.copyButton.title`.
- **Keys should be in camelCase**.
- **ICU Message Syntax**: Each key’s value should follow the [ICU Message Syntax](https://next-intl-docs.vercel.app/docs/usage/messages#rendering-icu-messages).
- **Add new keys at the bottom** of `i18n/locales/en.json` to help translators quickly identify recent additions.

### Notes on Nested Translation Keys

We use nested keys within locale files. If a key is `components.common.myComponent.something`, it should be defined within:

```json
{
  "components": {
    ...,
    "common": {
      ...,
      "myComponent": {
        "something": "value of translation key"
      }
    }
  }
}
```

---

## Translations and Unit Testing

Translation keys should not be translated during unit tests. If your component uses `useTranslations`, provide `<NextIntlProvider>` around your `testing-library` render logic, or create a wrapper for the test. 

**Important Unit Testing Considerations:**

- Tests should verify component functionality, not specific text or strings, as these can change and cause tests to fail.
- Use `aria-*` attributes, class names, or other artifacts rather than text for assertions.
- Use visual regression testing to validate how different languages and text appear within a component.