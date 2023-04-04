[Stable Diffusion web UI (AUTOMATIC1111) の使い方](https://note.com/npaka/n/nc8b0e9a91d97)

# Running
```
$ git clone https://github.com/AbdBarho/stable-diffusion-webui-docker.git
$ cd stable-diffusion-webui-docker
$ docker compose --profile download up --build
(GPU)(nvidia recommend)
$ docker compose --profile auto up --build
(CPU)(if not have gpu)
$ docker compose --profile auto-cpu up --build
```

# Explanation
**Sampling steps**
- Think of this as how long the AI spends working on the image. General rule of thumb is the more steps the higher quality. But this has diminishing returns as you go up.
- Start with 28 (Maximum 150).

**CFG Scale**
- Scale, also known as CFG scale, is how “focused” you want the AI to be on your prompt. 
- A higher value means the AI will be stricter about staying with your prompt. A lower value means it will have more freedom to deviate from your prompt. A good range to start is 5-15.
- Personally I like using lower scale, around 4-7, because I like giving the AI room to give me results I don’t expect.

**Sampling**
- How the AI thinks about your image: 
- k_euler is popular because it generally produces consistent, predictable results.
- ddim can be quite expressive and artistic.

**Seed**
- The way that these generators work is they start from a noise image (which is just that, literally noise):And then every step, they make the noise image look more and more like something that the model “knows” about.
- Each seed value corresponds exactly with a unique starting noise image.
- This means you can generate the same image as another user (with 90%-100% accuracy) if you use the same settings, same prompt, and same seed.
- Controlling for the same seed, and tweaking all of the other settings is a great way to see how each of the different settings impact the final image.
- You would get the exact same image if you used my exact settings.
- Practically, that means knowing the seed is critical if you want to duplicate another user’s image exactly.

**Prompt:**
- {{{masterpiece}}}, {{{best quality}}}, {{ultra-detailed}}, {cinematic lighting}, {illustration}, {beautiful detailed eyes}, {1girl}, upper body, looking at viewer, depth of field

**Undesired Content (Negative Prompt):**
- lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, fewer digits, cropped, worst quality, low quality, normal quality, jpeg artifacts, signature, watermark, username, blurry, artist name

**Settings:**
- Training set: NAI Diffusion Anime (Full)
- Steps: 40 (start lower at 28 so you don’t burn your Anlas)
- Scale: 7
- Sampling: k_euler
- {{swimsuit}}, {{{masterpiece}}}, {{{best quality}}}, {{ultra-detailed}}, {cinematic lighting}, {illustration}, {beautiful detailed eyes}, {1girl}, upper body, looking at viewer, depth of field
- {{school uniform}}, {{{masterpiece}}}, {{{best quality}}}, {{ultra-detailed}}, {cinematic lighting}, {illustration}, {beautiful detailed eyes}, {1girl}, upper body, looking at viewer, depth of field

## Using Quality & Detail Tags
There’s a ridiculous number of quality tags you can try and also mix together for interesting results:

- detailed
- hyper
- intricate
- wonderful
- accuracy
- amazing
- wonder
- finely
- super
- exquisitely

Here’s an example where I’ll keep the other settings exactly the same but change the quality descriptor.
- Undesired content (negative prompts): None
- Training set: NAI Diffusion Anime (Full)
- Add Quality Tags: Off (we’ll be using our own)
- Steps: 28
- Scale: 12
- Sampling: k_euler
- Seed: 2000000
- Prompt:
  - diamond
  - diamond, best quality
  - diamond, detailed
  - diamond, hyper detailed
  - diamond, masterpiece
  - diamond, intricate
  - diamond, wonderful detailed
  - diamond, amazing intricate finely detailed
  - diamond, hyper intricate fine detail

## Using More Emphasis Tags
If your images don’t look as good as you want them to, try adding more curly braces {} around your masterpiece tag.

Curly braces add emphasis and we’re just telling the AI we want a higher-quality image.

You can also add them to quality descriptors such as best quality and ultra-detailed, as well as things you feel are underemphasized in your generations.

{{{{{{{{{{{masterpiece}}}}}}}}}}},  {{{{{{swimsuit}}}}}}, {{{{{ultra-detailed}}}}}, {cinematic lighting}, {illustration}, {beautiful detailed eyes}, {1girl}, upper body, looking at viewer
- Training set: NAI Diffusion Anime (Full)
- Steps: 50
- Scale: 7
- Sampling: k_euler
- Note: the masterpiece and best quality and other quality tags will steer the AI away from things that are considered undesirable as well as things that are less common. If you are trying to generate a niche subject, you should actually avoid these tags!

## Undesired Content (Negative Prompts)
Getting too many mutated body parts?

Here are some negative prompts you can use to avoid different things (undesired content field). Click on headers to expand sections:

**Whole body (avoid mutated)**
- {long body}, bad anatomy , liquid body, malformed, mutated, bad proportions, uncoordinated body, unnatural body, disfigured, ugly, gross proportions ,mutation, disfigured, deformed, {mutation}, {poorlydrawn}

**Hands (avoid mutated)**
- { long body }, bad anatomy , liquid body, malformed, mutated, anatomical nonsense ,bad proportions, uncoordinated body, unnatural body, disfigured, ugly, gross proportions ,mutation, disfigured, deformed, { mutation}, {poorlydrawn}

**Hand held weapons (avoid fusing)**
- bad weapon, fused weapon, extra weapons, poorly weapon, bad sword, poor sword,

**Face (avoid poor quality)**
- liquid tongue, long neck, fused ears, bad ears, poorly drawn ears, extra ears, liquid ears, heavy ears, missing ears, fused animal ears, bad animal ears, poorly drawn animal ears, extra animal ears, liquid animal ears, heavy animal ears, missing animal ears, bad hairs, poorly drawn hairs, fused hairs, bad face, fused face, poorly drawn face, cloned face, big face, long face, bad eyes, fused eyes poorly drawn eyes, extra eyes, bad mouth, fused mouth, poorly drawn mouth, bad tongue, big mouth

**Leg (avoid mutated)**
- huge thighs, huge calf,disappearing thigh, disappearing calf, disappearing legs, malformed feet, extra feet, bad feet, poorly drawn feet, fused feet, missing feet, extra shoes, bad shoes,fused shoes, more than two shoes, poorly drawn shoes, missing thighs, missing calf, missing legs, missing legs, extra thighs, more than 2 thighs, extra calf,fused calf, extra legs, bad knee, extra knee, more than 2 legs, bad thigh gap, missing thigh gap, fused thigh gap, liquid thigh gap, poorly drawn thigh gap

**Clothes (avoid fusing)**
- fused clothes, poorly drawn clothes

## Art Styles
There are as many art styles you can try as there are stars in the sky. Here’s the same character with the same settings, in different art styles:

**Settings:**
- Undesired content (negative prompts): None
- Training set: NAI Diffusion Anime (Full)
- Add Quality Tags: Off (we’ll be using our own)
- Steps: 28
- Scale: 12
- Sampling: k_euler
- Seed: 121000000

**Base prompt:**
- 1girl, masterpiece, black hair

**Results with base prompt + art style modifier:**
- { watercolor }
- { gouache }
- { oil painting }
- { etching }
- { flat color }
- { line art }
- { 1990s }
- { hyperrealistic }
- { game cg }
- { ink wash }
- { painting (medium) }
- { pixel art }
- { tarot }
- { Ukiyo-e }
- { yoji shinkawa }

## A Note on RNG
There’s a huge random component (RNG) to image generation.

When you see people posting their images online, they are posting the best of the best.

(I’m only posting the better images I get in this guide as well).

**You’ll get LOTS of bad results too.** Even if you use the exact prompts you copy from online. It’s all part of the experience.

All the more reason to set your steps lower so you don’t use up your Anlas.

# Character Prompting
## Existing Characters
Results will vary wildly depending on the character.

For some, all you have to do is prompt character name for great results.

Others, you will have to prompt the character’s name as well as describe their characteristics.

There is only one correct way to write the character’s name. you want to use the name the character is tagged with on Danbooru.

eg. using yorha no. 2 type b will produce good results, however using 2b will not.

(You can see what version of the name NovelAI uses by letting it auto-complete the tag.)

Here’s a list of [the most popular characters on Danbooru](https://danbooru.donmai.us/tags?commit=Search&search%5Bcategory%5D=4&search%5Bhide_empty%5D=yes&search%5Border%5D=count). You can assume if the character has a substantial number of Danbooru images, NovelAI will generate them well. Remember to remove the underscores from the character’s name when you are using them in tags.
- Undesired content (negative prompts): Low Quality + Bad Anatomy (Preset)
- Training set: NAI Diffusion Anime (Full)
- Add Quality Tags: On
- Steps: 28
- Scale: 15
- Sampling: k_euler
- Prompt:
  - fujiwara no mokou, masterpiece
  - saber, masterpiece
  - yorha no. 2 type b, blindfold, black dress, black stockings, frills, {masterpiece}
  - akiyama mio, masterpiec
  - asuna (sao), masterpiece
  - hatsune miku, masterpiece
  - izayoi sakuya, masterpiece
  - ayanami rei, masterpiece
  - souryuu asuka langley, masterpiece

# Multiple Characters
You can make multiple characters appear with this prompt:
- 2girls_A_and_B, Agirl have blonde twintails and blue eyes, {master piece}, {extremely detailed}, Bgirl have short black hair and red eyes
- Undesired content (negative prompts): Low Quality + Bad Anatomy (Preset)
- Training set: NAI Diffusion Anime (Full)
- Add Quality Tags: On
- Steps: 28
- Scale: 15
- Sampling: k_euler

As usual, the more details you add the less stable the generations become (more propensity for weirdness).

You can see the eye colors are swapped from my prompt. This one will take a few rolls to get right.

## Faces
You can try the following expressions:
- :3
- happy
- evil smile
- serious
- unamused
- surprised
- laughing
- 

## Poses
You can try the following poses:
- looking back
- head rest
- on all fours
- wariza
- hugging own legs

# Environment Prompting
## Backgrounds

- classroom
- stained glass
- greenhouse
- bedroom
- cafe
- bookstore
- bakery

Outdoors:
- Forest
- lunar surface
- stratosphere
- underwater
- snowy
- atrium
- sunlight filtering through the trees

## Composition / Perspective
- close-up
- portrait
- upper body
- cowboy shot
- full body
- lower body

## Camera Effects
Depth of field: a good all-round addition to create the clear subject/blurry background photography effect.
- {{depth of field}}, hatsune miku, outside, sunny day, {masterpiece}

You can also specify different camera lens, starting from 20mm and going to 200mm

You can see that more zoom not only gives you camera effects, but increases the realism of the image as well:
- 20mm, portrait, girl, outside, sunny day, {masterpiece}
- 20mm,35mm,100mm,200mm


### Ref
- [Tutorial](https://aituts.com/anything-anime-stable-diffusion/)
- [The Complete NovelAI Prompt Guide](https://aituts.com/novelai-anime-prompt-techniques/)
- [魔術書](https://p1atdev.notion.site/p1atdev/611b109989c54ffca6219edd95d1b247)
- [LoRA](https://stable-diffusion-art.com/lora/)
- [DepthToImage](https://stable-diffusion-art.com/depth-to-image/)
- [Anything V5](https://civitai.com/models/9409)


## LoRA
- [Shukezouma LoRA](https://civitai.com/models/12597/moxin)
- [GuoFeng3](https://civitai.com/models/10415)

## Models to try next
There are a couple of other great models you can try:

[**OrangeMix**](https://huggingface.co/WarriorMama777/OrangeMixs) is a collection of models created by merging other models.

[**BloodOrangeMix**](https://huggingface.co/WarriorMama777/OrangeMixs#bloodorangemix) is quite popular in the Japanese SD community and very good quality.

Check this [full list of anime models](https://rentry.org/sdmodels) for more.

