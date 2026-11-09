# Concept 2: Flags Through Color-Blind Eyes

## The concept
**Identifying every countrys' flag based on their colors and understanding is its hard to tell apart or if they lose their meaning for people who are color blind**

This project takes images of every country's flag, converts them into how they look with each main type of color blindness, and measures which colors and flags collapse together.

**Factors in measurement**:
- Which flag colors merge for each type of color blindness
- Which pairs of flags become nearly identical
- Whether some regions or color combinations are affected more than others
- What color rules designers could follow to keep flags, maps and charts readable

## Relevance

About 1 in 12 men and 1 in 200 women are color blind, roughly 300 million people worldwide ([Live Science](https://www.livescience.com/health/genetics/why-is-color-blindness-so-much-more-common-in-men-than-in-women)). Flags appear on maps, sports broadcasts, language menus and travel apps, so flags that can't be told apart are an everyday design problem.

## Data

[Country flag images](https://hampusborgos.github.io/country-flags/) (PNG, public domain, named by country code), one flag image, about 250 flags 
[UCI Flags dataset](https://archive.ics.uci.edu/dataset/40/flags), one country, with its flag's colors, stripes, symbols and region, 194 countries 

### Color-blindness simulation (given to me by Claude and the answer it gave me)

The [Machado, Oliveira & Fernandes model](https://www.inf.ufrgs.br/~oliveira/pubs_files/CVD_Simulation/CVD_Simulation.html) (IEEE, 2009) gives ready-made 3×3 tables of numbers for each type of color blindness. Converting a pixel is one small calculation on its R, G and B values, the same pixel loop as Homework04. It covers the three main types:

- **Protanopia:** reds look darker and close to greens
- **Deuteranopia:** greens and reds merge (the most common type)
- **Tritanopia:** blues and yellows are confused (rare)

**Key decision:** I'll resize every flag to the same size, like Homework06A, and compare flags by their main colors rather than pixel by pixel, so a flag's shape doesn't hide a color problem.

## Method

1. **Collect** the flag images and the UCI table, and match them by country.
2. **Find each flag's main colors** by resizing it and counting which colors cover the most pixels.
3. **Simulate** every flag for protanopia, deuteranopia and tritanopia.
4. **Measure** how far apart each flag's colors are before and after, using the distance formula on R, G and B (the same formula as the Homework02 city distances), and find flag pairs that become nearly identical.
5. **Rank and predict:** sort flags by how much they lose, compare regions and color combinations, and test whether a simple classifier can predict "at-risk" flags from the UCI attributes better than a random guess.
6. **Design** a gallery of the most affected flags and a short set of color rules for designers.

## Deliverables

**The final**

- The full analysis notebook for all flags and all three types
- A ranking of the most and least affected flags, and a comparison by region
- The "at-risk flag" classifier, compared with random guessing
- **An interactive gallery- website form** where you pick a flag and see it through each type of color blindness, plus **color rules for designers** of maps, apps and charts, each linked to a finding

## How I'll use an LLM and show understanding

I'll use an LLM for code, with permission, and ways I'll use an LLM:

- **A criteria notebook** written before any code, quoted in every LLM request.
- **A decision log** of what the LLM suggested, what I kept or rejected, and why.
- **Hand checks**, such as testing the simulation on pure red, green and blue and comparing a few flags with published color-blind examples.
- **Baselines**

## Sources

- [Country flags](https://hampusborgos.github.io/country-flags/) (public-domain flag images by country code)
- [UCI Machine Learning Repository: Flags](https://archive.ics.uci.edu/dataset/40/flags) (194 countries, 30 attributes)
- [A Physiologically-based Model for Simulation of Color Vision Deficiency](https://www.inf.ufrgs.br/~oliveira/pubs_files/CVD_Simulation/CVD_Simulation.html) (Machado, Oliveira & Fernandes, IEEE TVCG 2009)
- [Why is color blindness so much more common in men than in women?](https://www.livescience.com/health/genetics/why-is-color-blindness-so-much-more-common-in-men-than-in-women) (Live Science)
