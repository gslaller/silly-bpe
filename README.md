# silly-bpe
## Prerequisite for this project.
If you have ever worked with any NLP project, you certainly came across tokenizer like BPE(Byte Pair Encoding). This preprocess gives the model a fixed number of tokens over which they have to train/predict. Other reasons being:
1. Dissects large or unseen words into smaller substrings called **tokens**.
    1. "My name is Gurpreet Singh." -> "My| name| is| Gur|p|reet| Singh|."
2. Is helpful for **Scriptio continua**, languages with compound nouns or multi lingual datasets.
    1. "Anpassungsmaßnahmen" -> "An|pass|ung|s|ma|ß|nah|men".
    2. "ਪੰਜਾਬ ਉੱਤਰ-ਪੱਛਮੀ ਭਾਰਤ ਦਾ ਇੱਕ ਰਾਜ ਹੈ" -> to 57 tokens.

Though these preprocess is **neccesary**(unless you want to go to byte|character level), they sometime have really odd or specific tokens like:
| Token | Token ID |
| --- | --- |
| " --------------------------------\n" | 20368 |
| "......" | 16317 |
| "=\\\" | 17553 |
| "________________________________________________________________" | 27193 |
| "OUP" | 27755 |

## The idea for this project
**The user picks the silliest token and we rank these tokens with the ELO scoring.**  
You can visit the project(when ready) on this [skriving.com/silly-bpe](http://skriving.com/silly-bpe).



## ELO ranking:
My reference to ELO rating mechanism: [metinmediamath](https://metinmediamath.wordpress.com/2013/11/27/how-to-calculate-the-elo-rating-including-example/)

1. $$R(1) = 10^{r(1)/100}$$   
$$R(2) = 10^{r(2)/100}$$

2. $$E(1) = \frac{R(1)}{R(1) + R(2)}$$  
$$E(2) = \frac{R(2)}{R(1)+R(2)}$$

3. Now we wait for the match to finish and set the actual score int he third step.
    1. if player 1 wins $$S(1) \equiv 1$$
    2. if player 1 wins $$S(2) \equiv 0$$
    3. equivalent if player 2 wins
4. $$r'(1) = r(1) + K * (S(1) - E(1))$$  
$$r'(2) = r(2) + K * (S(2) - E(2))$$

## online tools and data:
1. [gpttools.com](https://gpttools.com/estimator).
2. [openai's tokenizer](https://platform.openai.com/tokenizer).
3. [english volac](https://raw.githubusercontent.com/openai/whisper/main/whisper/assets/gpt2/vocab.json) used for english only [whisper (ASR)](https://github.com/openai/whisper).
4. [multilingual volac](https://raw.githubusercontent.com/openai/whisper/main/whisper/assets/multilingual/vocab.json) used for multi language [whisper (ASR)](https://github.com/openai/whisper).
