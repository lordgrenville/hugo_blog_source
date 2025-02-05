+++
title = "Haftorah Stats"
author = ["Josh Friedlander"]
date = 2025-02-05
draft = false
+++

## Background {#background}

The custom of reading a passage from the Prophets, the _haftorah_, is ancient and obscure. The Talmud deals with it{{< sidenote >}}Megilla 31a{{< /sidenote >}} but does not elaborate on the source or the reason for the custom. According to one early source{{< sidenote >}}Tosfos Rid (R’ Yeshaya MiTrani) in _Sefer HaMachria_ 31{{< /sidenote >}}, it is no less old than the custom of public Torah reading itself, traditionally held to have been instituted by Ezra.

This post will not shed any light on these questions, but instead answer a far simpler one: how are the haftarot of the annual cycle distributed between the different books of the Prophets? As "all are subject to luck, even the Torah scroll in the ark"{{< sidenote >}}Zohar Bamidbar 134a{{< /sidenote >}}, which books are fortunate enough to be read more often than others?

To this end I put together a [table of the annual readings](https://github.com/lordgrenville/haftarot/blob/main/haftarot.csv) and did a quick data analysis{{< sidenote >}}Code and data to reproduce are available [online](https://github.com/lordgrenville/haftarot). I will gratefully receive any corrections or suggestions.{{< /sidenote >}}. For each book I calculated the number of _haftarot_ it has, number of chapters, and the ratio of the two (to give a sense of _haftorah_ frequency relative to size). My takeaways were:

-   The biggest single source of haftarot is Yeshayahu. (With the שבע דנחמתא freshly behind us, this may not feel surprising!)
-   When measuring relative to size, Trei Asar as a whole is the largest (scoring 0.36), with multiple haftarot coming from Hoshea, Amos and Zecharia, while the books of Ovadia and Yona are read in their entirety. (Yoel contributes just a snippet at the end of the _haftorah_ of _Shabbos Shuva_, while Nachum, Chavakuk, Tzafania and Chagai are entirely absent.)
-   However, if considered separately, both Malachi (0.67) and Melachim Alef (0.45) have higher scores.
-   If we take “Deutero-Isaiah” (ישיעהו השני){{< sidenote >}}Chapters 40-66, which differ from the first part in both style and chronology{{< /sidenote >}} as an independent book, it is the largest single source of haftarot (15, scoring 0.58). In fact, the rest of Yeshayahu has a mere 3 haftarot, giving it the lowest score (0.08) of any book. (But one of these is the famous reading of _Shabbos Chazon_, which surely counts for something…)
-   There are roughly twice as many haftarot from the (mostly non-narrative){{< sidenote >}}A generalisation: there are some narrative parts in the Latter Prophets (e.g. Yeshayahu 36, all of Yona), and some non-narrative parts in the Early Prophets.{{< /sidenote >}} Latter Prophets compared to the Early Prophets (50 vs 26). This is partly due to their greater length, and partly, I suspect, because it is harder to find thematic overlap between narrative prophecies and the weekly Torah portions.


## Results {#results}

| Book | Number of Haftarot | Number of Chapters | Haftarot:Chapter ratio |
|:---------|:--------------------:|:--------------------:|:------------------------:|
| תרי עשר | 13                 | 36                 | 0.361                  |
| מלכים   | 13                 | 45                 | 0.289                  |
| ישעיהו  | 18                 | 66                 | 0.273                  |
| יחזקאל  | 10                 | 48                 | 0.208                  |
| ירמיהו  | 9                  | 52                 | 0.173                  |
| שופטים  | 3                  | 21                 | 0.143                  |
| שמואל   | 7                  | 53                 | 0.132                  |
| יהושע   | 3                  | 24                 | 0.125                  |


## Notes on Methodology {#notes-on-methodology}

I took the list of _haftarot_ from [here](https://www.shoresh.org.il/usersfiles/articlesdocs/parashot.pdf). In cases where customs differ, I followed the Ashkenazi rite (there are only a few cases where different communities read from entirely different books). I included Rosh Chodesh and holiday readings, but not that of יום עצמאות. If a haftorah included parts from different books, I included only the main part of the reading.
