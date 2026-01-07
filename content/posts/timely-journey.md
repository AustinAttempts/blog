---
date: '2026-01-06T15:44:27-08:00'
title: 'Austin Attempts: Timely Journey'
author: ["Austin Guevara"]
type: "post"
---

The only things provided by this puzzle are the Title: "Timely Journey" the below image, and a PDF copy of the paper seen in the image.

<img src="/imgs/timely-journey/timely-journey.jpg#center" alt="Timely Journey Puzzle Image">

I also checked the webpage using Chrome DevTools Inspect Mode to see if any hidden text was present but did not notice anything unusual.  Therefore my assumption is that everything needed to solve this puzzle is contained withing the image and the title is most likely a hint.

# Searching for Clue

Other than the Sheet of Paper (the associated PDF) I count 7 potnential clues in the image.

{{< notice info >}}
I think the Sheet of Paper looks like a crossword puzzle so I will refer to it as such from here on.
{{< /notice >}}

## Point of Interest 1: Colored Push Pins

<img src="/imgs/timely-journey/tacks.png#center" alt="cup of colored push pins">

This is a cup of colored push pins with colors red (orange), blue, green, white, black, yellow, purple and transparent.  The only thing that stands out to me is the top of this pile has two blue pins sandwhiched between red pins.  Because Blue and Red are prevalent colors crossword this may be important.

### Potential Takeaways:
- Blue between Red

## Point of Interest 2: Scrabble Tiles

<img src="/imgs/timely-journey/scrabble.png#center" alt="Scrabble tiles">

The Scrabble tiles show a relation between a numeric value and an English Letter.  Considering the crossword seems to only have numeric values I am leaning towards this being the key to a cipher to help decrypt the sets of numbers on that sheet.  The shown tiles are C3, J8, S1.

- C3: C is the third letter of the alphabet. Perhaps A1Z26 Cipher?
- J8: J is the 10th letter so A1Z26 no longer likely
- S1: S is the 19th letter so definitly not A1Z26

These are all valid Scrabble Tiles so we can check the rest of the tiles:

| Score | Letter |
|:------:|:-------:|
| 1 | A, E, I, L, N, O, R, S, T, U |
| 2 | D, G |
| 3 | B, C, M, P |
| 4 | F, H, V, W, Y |
| 5 | K |
| 6 | |
| 7 | |
| 8 | J, X |
| 9 | |
| 10 | Z |

The crossword has only values 0-9 so if this table maps correcly I will have to add 1 to each number on the crossword. However, the crossword has values 5, 6, and 8 which would then have unmapped values.  These unmapped values could potentially be a space (' '), but I find this an unlikly key to decoding the values.

There is one other tile face up but partially covered. The tile is an 'I' however the score is not visible and and because it is placed horizontally it looks more like a '-'.  This potentially could mean a '0' represents a space or dash.

### Potential Takeaways:
- C3, J8, S1, maybe _0???
- 381
- CJS

## Point of Interest 3: Dominoes

<img src="/imgs/timely-journey/dominoes.png#center" alt="Dominoes">

There are three face up dominoes showing 2-0, 1-6, 0-4.  The colors on these seem irrelevant to me for now. Reading left tor right these could represent that 2 -> 0, 1 -> 6, 0 -> 4.  Since this would cause a state where 2 -> 0 -> 4 I do not think this is a proper interpertation.

### Potential Takewaways:
- Nothing so far

## Point of Interest 4: Dice

<img src="/imgs/timely-journey/dice.png#center" alt="Dice">

Because there is one Blue Dice and one Red Dice I think this hint is related to how to interpert the colored sections of the crossworld.

- The Blue dice appears to be a D48 with either the value 7 or 20 showing on top. (the 7 could be a 1)
- The Red dice appears to be a D60 with the value 56 showing on top.

### Potential Takewaways:
- Blue values related to 48, 7, 20, or 1
- Red values related to 60 or 56

## Point of Interest 5: Hello...

<img src="/imgs/timely-journey/hello.png#center" alt="Hello...">

There is a Box with a shelf sticking out that says "Hello..." in a speech bubble. No idea what this could mean yet.

### Potential Takewaways:
- Nothing so far

## Point of Interest 6: Colored Dice

<img src="/imgs/timely-journey/colored-dice.png#center" alt="Colored Dice all on 1">

There are 8 6-sided dice all showing the value 1.  The colors on this seem irrelevant to me for now.

### Potential Takeaways:
- 8 and 1 being related somehow

## Point of Interest 7: Plant Box

<img src="/imgs/timely-journey/plant-box.png#center" alt="Plant Box">

This box has some text on it that I can barely make out. From what I can see the Logo says: "Minnesota State High School" on top and "... Leage" on the bottom. Below the Logo is "1998 Twin Cities Private Division".  This is all I can read.  Because the title of the Puzzle is "Timely Journey" It may be possible the year 1998 is relevant to timely and Twin Cities is relevant to Journey.

### Potential Takeaways:
- Twin Cities
- 1998

# Cross Word Analysis

<img src="/imgs/timely-journey/jan-2026-timely-journey.pdf#center" alt="crossword puzzle">

The Crossword puzzle seems to be the primary focus of this puzzle.  There are 2 chunks of digits; one in the top right and the other in the bottom left.  The rest of the page is an empty crossword grid.  Certain cells in the grid are colored Red and Blue just like certain digits in the chunks are colored Red and Blue.

## Empty Crossword Grid Notes
- 12 vertical "words" comprised of 98 cells
- 12 horizontal "words" comprised of 89 cells
- 24 Red cells
- 24 Blue cells
- ?? total cells

## Top Right Chunk Notes
- 77 total digits
- digits ranging from 0-9
- 12 columns of digits
- columns length varying from 5-7 digits
- 12 red digits
- 13 blue digits

## Bottom Left Chunk Notes
- 70 total digits
- digits ranging from 0-9
- 12 rows of digits
- row length varying from 5-6 digits
- 12 red digits
- 12 blue digits

## Assumptions
- The digits do not map 1:1 to the crosswords cells
    - The Red and Blue Cell counts don't align with the Red and Blue Digit counts
    - The total digit counts don't align with the total cell counts
- The top right chunk are hints for the vertical words
- the bottom left chunk are hints for the horizontal words
