---
project: Iosevka
stars: 21493
description: Versatile typeface for code, from code.
url: https://github.com/be5invis/Iosevka
---

* * *

**Iosevka** \[ˌjɔˈseβ.kʰa\] is an _open-source_, _sans-serif_ + _slab-serif_, _monospace_ + _quasi‑proportional_ typeface family, designed for _writing code_, using in _terminals_, and preparing _technical documents_.

Installation
------------

### Installing from GitHub Releases

1.  Download your font package from releases.

-   For Linux users you could use the following command to download all the TTC packages in the latest release:
    
    curl -s 'https://api.github.com/repos/be5invis/Iosevka/releases/latest' | jq -r ".assets\[\] | .browser\_download\_url" | grep PkgTTC-Iosevka | xargs -n 1 curl -L -O --fail --silent --show-error
    

1.  Quit all your editors / programs.
2.  Unarchive the font package and you will see the font files.
3.  Take actions depending on your OS:
    -   **Windows**: Select the font files and drag into font settings / font control panel page.
        -   On Windows 10 1809 or newer, the default font installation is per-user, and it may cause compatibility issues for some applications, mostly written in Java. To cope with this, right click and select “Install for all users” instead. Ref.
    -   **macOS**: Follow instructions here.
    -   **Linux** : Copy the font files to your fonts directory then run `sudo fc-cache`.

### Installing via Package Managers

_Disclaimer: This repository does not maintain any package manager distribution. The packages listed below may not always be up-to-date._

-   **macOS**
    -   Standard distribution in Homebrew:
        
        brew install --cask font-iosevka
        
    -   Search for other variants using `brew search font-iosevka` and install what you want.
    -   Customizable install using Homebrew: see robertgzr/homebrew-tap.
-   **Linux**
    -   Arch Linux: Install one of the ttc-iosevka packages.
    -   Ubuntu Linux: Install one of the fonts-iosevka packages.
    -   Void Linux: Install the font with `xbps-install font-iosevka`.
    -   Fedora: Install the font(s) from the COPR here. Run `dnf search iosevka` to discover available fonts and `dnf install` to install the chosen one(s).
-   **FreeBSD**: The font can be installed with `pkg install iosevka`.
-   **OpenBSD**: Run `pkg_info -Q iosevka` to see which Iosevka packages are available. Use `pkg_add` to install the chosen package(s).

Features
--------

In the official package, Iosevka provides 6 monospace subfamilies (sans-serif and slab-serif, each in the 3 spacings Default, Term and Fixed) and 2 quasi-proportional subfamilies (Aile (sans-serif) and Etoile (slab-serif)). In all the monospace subfamilies, 9 weights (Thin to Heavy), 2 widths (Normal and Extended), and 3 slopes (Upright, Italic and Oblique) are included. In the quasi-proportional subfamilies, the quantity of widths is reduced to 1.

All versions include the same ranges of characters: Latin letters, Greek letters (including Polytonic), some Cyrillic letters, IPA symbols and common punctuations and some symbols. You can check out the full list here.

241 Supported Languages:

Abkhazian, Afar, Afrikaans, Aghem, Akan, Akoose, Albanian, Anii, Aragonese, Armenian, Asturian, Asu, Atsam, Azerbaijani, Bafia, Baluchi (bal\_latn), Bambara, Basaa, Bashkir, Basque, Belarusian, Bemba, Bena, Betawi, Bosnian, Breton, Bulgarian, Caddo, Catalan, Cebuano, Central Atlas Tamazight, Chechen, Chickasaw, Chiga, Chinese (zh\_latn), Choctaw, Church Slavic, Chuvash, Colognian, Cornish, Corsican, Croatian, Czech, Danish, Duala, Dutch, Embu, English, Erzya, Esperanto, Estonian, Ewe, Ewondo, Faroese, Filipino, Finnish, French, Friulian, Fula, Ga, Galician, Ganda, German, Greek, Guarani, Gusii, Haitian Creole, Hausa, Hawaiian, Hindi (Latin), Hungarian, Icelandic, Ido, Igbo, Inari Sami, Indonesian, Interlingua, Interlingue, Inuktitut (iu\_latn), Irish, Italian, Javanese, Jju, Jola-Fonyi, Kabuverdianu, Kabyle, Kaingang, Kako, Kalaallisut, Kalenjin, Kamba, Kara-Kalpak, Kazakh, Kenyang, Kikuyu, Kinyarwanda, Konkani (kok\_latn), Koyra Chiini, Koyraboro Senni, Kpelle, Kurdish, Kuvi, Kwasio, Kyrgyz, Kʼicheʼ, Lakota, Langi, Latgalian, Latin, Latvian, Ligurian, Lingala, Lithuanian, Lojban, Lombard, Low German, Lower Sorbian, Luba-Katanga, Lule Sami, Luo, Luxembourgish, Luyia, Macedonian, Machame, Makhuwa, Makhuwa-Meetto, Makonde, Malagasy, Malay, Maltese, Manx, Mapuche, Masai, Meru, Metaʼ, Mi'kmaw, Mohawk, Moksha, Mongolian, Morisyen, Mundang, Muscogee, Māori, Nama, Navajo, Ngiemboon, Ngomba, Nheengatu, Nigerian Pidgin, North Ndebele, Northern Frisian, Northern Sami, Northern Sotho, Norwegian, Norwegian Bokmål, Norwegian Nynorsk, Nuer, Nyanja, Nyankole, Obolo, Occitan, Oromo, Ossetic, Papiamento, Pijin, Polish, Portuguese, Prussian, Quechua, Riffian, Romanian, Romansh, Rombo, Rundi, Russian, Rwa, Saho, Samburu, Sango, Sangu, Sardinian, Scottish Gaelic, Sena, Serbian, Shambala, Shona, Sicilian, Sidamo, Silesian, Skolt Sami, Slovak, Slovenian, Soga, Somali, South Ndebele, Southern Sami, Southern Sotho, Spanish, Sundanese, Swahili, Swati, Swedish, Swiss German, Tachelhit (shi\_latn), Taita, Tajik, Taroko, Tasawaq, Tatar, Teso, Tok Pisin, Toki Pona, Tongan, Tsonga, Tswana, Turkish, Turkmen, Tuvinian, Tyap, Ukrainian, Upper Sorbian, Uzbek, Vai (vai\_latn), Venda, Venetian, Vietnamese, Volapük, Vunjo, Walloon, Walser, Warlpiri, Welsh, Western Frisian, Wolof, Xhosa, Yakut, Yangben, Yoruba, Zarma, Zhuang, Zulu

### Stylistic Sets

Monospace Iosevka contains various stylistic sets to change the shape of certain characters. Enabling corresponded OpenType feature to enable.

View list of stylistic sets of Iosevka.
---------------------------------------

### Character Variants

Alongside stylistic sets, Monospace Iosevka can also be configured to cherry-pick variants for each character using OpenType. The variants are shown below. To enable, assign the feature tag to the variant index. For example, setting `cv26` to `6` will enable single-storey `a`.

**Caution :** Certain software may limit the quantity of OpenType features and drop some of them if the feature list is too long. Please validate your feature configuration to ensure that it worked in your software.

View list of character variants of Iosevka.
-------------------------------------------

### Ligations

Monospace subfamilies support ligations. Iosevka’s default ligation set is assigned to `calt` feature, though not all of them are enabled by default.

`calt off`

Ligation Off

`calt`

Default setting in text editors

`dlig`

Discretionary ligatures

Iosevka supports Language-Specific Ligations, which is the ligation set enabled only under certain languages. These ligation sets are assigned to custom feature tags. To use them, you need to turn **off** `calt` and enable the corresponded feature. The feature list is:

View list of language-specific ligations.
-----------------------------------------

Please note that, due to the complex interactions when forming ligations, cherry-picking ligation groups will require a custom Iosevka build. The instructions could be seen below.

Building from Source
--------------------

Read instructions.
------------------

For Chinese, Japanese and Korean (CJK) users...
-----------------------------------------------

→ Sarasa Gothic.

Mirrors
-------

-   TUNA (CN): https://mirrors.tuna.tsinghua.edu.cn/github-release/be5invis/Iosevka
-   NJU (CN): https://mirrors.nju.edu.cn/github-release/be5invis/Iosevka

* * *
