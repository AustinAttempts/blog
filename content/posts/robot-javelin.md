---
date: '2026-01-05T14:17:48-08:00'
draft: false
title: 'Austin Attempts: Robot Javelin'
author: ["Austin Guevara"]
type: "post"
math: true
---
## Jane Street's Robot Javelin Competition
 
 Unfortunatly, my entry for this puzzle was incorrect.  However, Here is my inital logic and thought process along with notes for where I went wrong.

 # Robot Javelin

There is a group of robots that compete to throw a javelin as far as possible in head-to-head (1v1) competitions.  The Robot that submits the longest throw wins the competition.

### Rules
1. Each competitor will throw their javelin once.
2. Based off the distance of their first throw the Robot will then decide if they want to keep that distance or rethrow.
3. If they rethrow they are required to submit the distance of the new throw.
4. The robot has no information on opponent's throws

### Givens
1. A robots throw is a random number drawn uniformly between $0$ and $1$.
2. The game has reached Nash Equilibrium and therefore all Robots are using the same strategy.

## Nash Equilibrium Strategy

As stated in the rules each Robot's actions are independent of their competitor.  This means that this strategy is purely based on increasing the probability of maximizing ones own score.  Because the first throw is purely random and required, all strategies would throw the first javelin then the strategy would be whether or not they throw the javelin again or keep your first distance.  In a unifrom distribution of distances a distance of $0.5$ is the mid midpoint.  This means that a new throw has a $50\%$ chance to be less than $0.5$ and a $50\%$ chance to be greater than $0.5$.  Based on this the Robot should only ever rethrow if their is a greater than $50\%$ chance that the rethrow will improve their score.

{{< notice info >}}
This was the assumption that caused me to get the wrong answer.  The actual Nash Equilibrium strategy is to rethrow only if the first throw is less than $(\sqrt{5} - 1) \div{2} \approx 0.618034 (\phi)$.
{{< /notice >}}

### Simplified Strategy
```
let x = distance of first throw
if (x < 0.5) rethrow else keep first throw
```

### Case 1: Both Robots first throw is less than 0.5

- Player 1's first throw is under the $0.5$ threshold which means the probability of improving its distance is greater than $50\%$ so it rethrows.
- Player 2's first throw is under the $0.5$ threshold which means the probability of improving its distance is greater than $50\%$ so it rethrows.
- Both Players now have complty random throws between $[0, 1]$ so there is a 50/50 odds of winning

### Case 2: Both Robots first throw is greater than 0.5

- Player 1's first throw is over the $0.5$ threshold which means the probability of improving its distance is less than $50\%$ so keep this distance.
- Player 2's first throw is over the $0.5$ threshold which means the probability of improving its distance is less than $50\%$ so keep this distance.
- Both Players now have complty random throws between $[0.5, 1]$ so there is a 50/50 odds of winning

### Case 3: Player 1's first throw is less than 0.5 and Player 2's first throw is greater than 0.5

- Player 1's first throw is under the $0.5$ threshold which means the probability of improving its distance is greater than $50\%$ so it rethrows.
- Player 2's first throw is over the $0.5$ threshold which means the probability of improving its distance is less than $50\%$ so keep this distance.
- Player 1 has a throw distance between $[0, 1]$ and player 2 has a throw distance between $[0.5, 1]$ so Player 1 wins $25\%$ of the time & Player 2 wins $75\%$ of the time.

### Case 4: Player 1's first throw is greater than 0.5 and Player 2's first throw is less than 0.5

- Player 1's first throw is over the $0.5$ threshold which means the probability of improving its distance is less than $50\%$ so keep this distance.
- Player 2's first throw is under the $0.5$ threshold which means the probability of improving its distance is greater than $50\%$ so it rethrows.
- Player 1 has a throw distance between $[0.5, 1]$ and player 2 has a throw distance between $[0, 1]$ so Player 1 wins $75\%$ of the time & Player 2 wins $25\%$ of the time.

### Truth Table

let *a* = Player 1's first throw\
let *b* = Player 2's first throw

| *a* | *b*| Player 1 wins | Player 2 wins |
|:----------------:|:----------------:|:-------------:|:--------------:|
|≤ 0.5             | ≤ 0.5            | 50%           | 50%            |
|> 0.5             | > 0.5            | 50%           | 50%            |
|≤ 0.5             | > 0.5            | 25%           | 75%            |
|> 0.5             | ≤ 0.5            | 75%           | 25%            |


### Probability of each case:

- **Case 1:** $P(a ≤ 0.5) × P(b ≤ 0.5) = 0.5 × 0.5 = 0.25$
- **Case 2:** $P(a > 0.5) × P(b > 0.5) = 0.5 × 0.5 = 0.25$
- **Case 3:** $P(a ≤ 0.5) × P(b > 0.5) = 0.5 × 0.5 = 0.25$
- **Case 4:** $P(a > 0.5) × P(b ≤ 0.5) = 0.5 × 0.5 = 0.25$

### Expected Win Rate of robot:

- **Case 1:** $0.25 × 0.5 = 0.125$
- **Case 2:** $0.25 × 0.5 = 0.125$
- **Case 3:** $0.25 × E[b | b > 0.5] = 0.25 × 0.75 = 0.1875$
- **Case 4:** $0.25 × E[1-a | a > 0.5] = 0.25 × 0.25 = 0.0625$

## Spears Robot vs Nash Equlibrium
$ 0.125 + 0.125 + 0.1875 + 0.0625 = 0.5 \text(50\%) $

# Spears Robot

One Robot, Spears Robot, has managed to break away from the "honorable" play that the rest of the competition has subscribed to.  This robot has managed to get one extra bit of data based off their opponents first throw.  Spears Robot is allowed to know if their opponent has surpassed some value of $x$.

## Assumptions

- Spears Robot knows the robot it is playing against is using the aformentioned Nash Equilibrium Strategy.

## Spears Robot Strategy

Because Spears Robot knows the Nash Equilibrium Strategy it can predict exaclty what its opponent will do if it sets $x$ to $0.5$.  This way it knows if its opponent is keeping its first throw or rethrowing and base it's decision making on that.

### Case 1: Spears Robot first throw is less than 0.5

Just like the Nash Equilibrium Strategy Spears Robot is more likely to improve its score by rethrowing. This will be the case whether or not its opponent has suprassed the threshold value of $x$ so this case is independant of the opponents first throw.

### Case 2: Spears Robot first throw is greater than 0.5

This scenario is where Spears Robot can take advantage of the threshold value $x$ being surpassed or not and change its behaviour based on that.  This will then break down into two possibilites:

#### 1: Opponent **under** $x$ threshold

In this case the opponent will attempt a rethrow to improve their score which will give the opponents end result a possible value $[0, 1]$ while Spears Robot will have a final score $[0.5, 1]$.  Therfore, Spears Robot should not rethrow and keep its first throw making this identical to the Nash Equilibrium Strategy.

#### 2: Opponent **over** $x$ threhshold

Here is the scenario where Spears Robot can make the most of the advantage of knowing if it's opponent has surpassed the threshold value $x$. In this case both Robots have surpassed the threhsold and now have scores $[0.5, 1]$.  Because this result should equate to a 50/50 winning chance Spears Robot will now switch to a more aggressive reroll strategy.

If the opponent has a score $[0.5, 1]$ and Spear Robot rerolls it will:
- automatically lose is new throw is $< 0.5$
- have a 50/50 chance of winning if throw is $≥ 0.5$
- **Total Win Probability:** $0.5 \times 0.5 = 0.25 \text{(25\%)}$


If Spears robot keeps its score:

$$
P(\text{Win}) = \frac{x - 0.5}{1 - 0.5} = 2x - 1
$$

This means that Spears Robot should only keep its score if the odds of winning with its current score is better than rerolling which we found to be $25\%$.

$$2x - 1 = 0.25$$
$$2x = 1.25$$
$$x = \mathbf{0.625}$$

Using this new threshold value we must recalculate the win probability in this matchup scenario.

let $a$ = Spears Robot's first throw

Given our new probability distribution is between $[0.5, 1]$ instead of $[0, 1]$ our equations can be adjusted to these two cases:

- Case: $0.5 ≤ a < 0.625$
    - $P(0.5 < a < 0.625) = \frac{0.625 - 0.5}{1 - 0.5} = \frac{0.125}{0.5} = 0.25$
    - $P(\text{Win}) = \frac{0.625 - 0.5}{1-0.5} = \frac{0.125}{0.5} = 0.25$
- Case: $0.625 ≤ a < 1$
    - $P(a ≥ 0.625) = \frac{1 - 0.625}{1 - 0.5} = \frac{0.375}{0.5} = 0.75$
    - $P(\text{Win}) = 2x - 1 = 2 \times \frac{1 + 0.625}{2} - 1 = 2 \times 0.8125 + 1 = 0.625$

This gives an updated win probability of:
$$
(0.25 \times 0.25) + (0.75 \times 0.625) = 0.0625 + 0.46875 = 0.53125
$$

{{< notice info >}}
Despite having the wrong inital strategy I was very close on the strategy that Spears Robot should use.  Spears should use a threhshold equivlaent to the Nash Equilibrium strategy but only rethrow if its first throw is below $0.5$, like I assumed, and if the opponents throw is above the Nash Equilibrium threhshold of $\phi$.  However, I did not realize this also recalcualtes its inital rethrow threshold.  The new rethrow threhsold on any throw musr be updated to $(1 - \frac{\phi}{2}) \approx 0.0.690983$.
{{< /notice >}}

### Simplified Strategy

```
let x = distance of Spears Robot's first throw
threhsold = if (opponent's first throw > 0.5) 0.625 else 0.5
if (x < threhshold) rethrow else keep first throw
```

### Truth Table

let *a* = Spears Robot's first throw\
let *b* = Oppnents's first throw\
let *t* = Spears Robot's threhshold value

| *a* | *b*| *t* |Spears Robots wins| Nash Equilibrium wins |
|:--------:|:----------:|:----:|:--------:|:---------:|
|≤ 0.5     | ≤ 0.5      | 0.5  | 50%      | 50%       |
|> 0.5     | > 0.5      | 0.625| 53.125%  | 46.875%   |
|≤ 0.5     | > 0.5      | 0.5  | 25%      | 75%       |
|> 0.5     | ≤ 0.5      | 0.5  | 75%      | 25%       |

## Spears Robot vs Nash Equlibrium

Since each of the 4 cases have an equal chance of occuring after the first throw the total win percentage of Spears Robot against a Nash Equilibrium Robot can be calculated as follows:

$$
0.25 \times (0.5 + 0.53125 + 0.25 + 0.75) = 0.5078125 \text{ (50.7\%)}
$$

# Java Lin

A robot named Java Lin discovers that Spears Robot is cheating.  Java lin is aware that Spears robot is receiving information on its opponents first throw and has adjusted its strategy accordingly.  Using this knowledge Java Lin has figured out the above strategy that Spears Robot is using and has developed a counter strategy to increase its odd of winning against Spears Robot.

## Assumptions

- Java Lin knows Spears Robots strategy
- Java Lin competes "honestly" and does not get the extra infromation that Spears Robot does about if its opponent has surpassed some distance $x$ on thei first throw
- Java Lin will only use this strategy against Spears Robots so it does not need to have an adavtange over the Nash Equilibrium strategy

## Java Lin Strategy

Java Lin's Best option to even the playing field against Spears Robot is to adjust its threshold for rethrows to more aggressivly target Spears Robot's assumptions.  However, it is important to note becuase of the lack of information compared to Spears Robot Java Lin will never be able to have a positive win probability it can only try to even the playfield.

### Java Lin's win probability when rethrowing

Spears Robot's strategy is dependnt on Java Lin's first throw so Java Lin's expected win rate is dependent on the first throw it is discarding with the rethrow.

1) Java Lin first throw $< 0.5$ (Spears Robot uses threhsold of $0.5$)
    - Java Lin will have a score $[0, 1]$ after the rethrow
    - Spears Robot has a $50\%$ chance to rethrow:
        - Spears Robot Rethrows ($50\%$): Both have scores $[0, 1]$ (Java Lin wins $50\%$)
        - Spears Robot Keeps ($50\%$): Spears Robot has scores $[0.5, 1]$ (Java Lin wins $25\%$)
    - $P(\text{Win}) = (0.5 \times 0.5) + (0.5 \times 0.25) = 0.375$
2) Java Lin first throw $\ge 0.5$ (Spears Robot is uses threhsold of $0.625$)
    - Java Lin will have a score $[0, 1]$ after the rethrow
    - Spears Robot has a $62.5\%$ chance to rethrow:
        - Spears Robot Rethrows ($62.5\%$): Both have scores $[0, 1]$ (Java Lin wins $50\%$)
        - Spears Robot Keeps ($37.5\%$): Spears Robot has scores $[0.625, 1]$ (Java Lin wins $18.75\%$)
    - $P(\text{Win}) = (0.625 \times 0.5) + (0.375 \times 0.1875) = 0.3828125$


### Java Lin's win probability when keeping

let $a$ = Java Lin's first throw distance

1) $a < 0.5$ (Spears Robot uses threhsold of $0.5$)
    - Java Lin only wins if Spears Robot rethrows ($50\%$) and gets a lower value $a$
    - $P(\text{Win}) = (0.5 \times a)$ since $a < 0.5$ $P(\text{Win}) < 0.25$
    - since $0.25 < 0.365$ Java Lin should never keep on a score $< 0.5$
2) $0.5 \le a \le 0.625$ (Spears robot uses threhshold of $0.625$)
    - Java Lin only wins if Spears Robot rethrows ($62.5\%$) and gets a value less than $a$
    - $P(\text{Win}) = (0.625 \times a)$

### Updated rethrow threshold

We can use these probailites to update our rethrow threshold for the best results possible.

$$P(\text{Win with keeping}) = P(\text{Win with rethrow})$$
$$0.625 \times a = 0.3828125$$
$$a = 0.6125$$

{{< notice info >}}
he correct Strategy here is similar to what I have above.  Java Lin should keep scores it would otherwise rethrow to take advantage of Spears Robot's rethrows.  However the correct range to keep is $[\frac{7}{12}, \phi]$.
{{< /notice >}}

### Simplified Strategy
```
let x = distance of first throw
if (x < 0.6125) rethrow else keep first throw
```

### Truth Table

let $a$ = Spears Robot's first throw\
let $b$ = Java Lin's first throw\
let $T_a$ = Spears Robots threshold (based off of $b$)
let $T_b$ = Java Lin's threhshold (constant)

| $a$ | $b$ | $T_a$ | $T_b$ | Spears Robot wins | Java Lin wins |
|:---:|:---:|:-----:|:-----:|:-----------------:|:-------------:|
|$\le 0.5$|$\le 0.5$| $0.5$ | $0.6125$ | $50\%$ | $50\%$ |
|$\le 0.5$|$> 0.5$| $0.625$ | $0.6215$ | $75\%$ | $25\%$ |
|$(0.5, 0.6125)$|$\le 0.625$| $0.625$ | $0.6125$ | $50\%$ | $50\%$ |
|$(0.5, 0.6125)$|$> 0.625$| $0.625$ | $0.6125$ | $81.25\%$ | $18.75\%$ |
|$\ge 0.6125$|$\le 0.625$| $0.625$ | $0.6125$ | $19.4\%$ | $80.6\%$ |
|$\ge 0.6125$|$> 0.625$| $0.625$ | $0.6125$ | $51.7\%$ | $48.3\%$ |

## Java Lin vs Spears Robot

let $a$ = Java Lin's first throw

1) Case: $0 \le a \le 0.5$ (Probability $50\%$)
    - Spears Robot rethrows ($50\%$): Both are $[0, 1]$ --> Java Lin wins %50\%$ of the time
    - Spears Robot keeps ($50\%$): Spears Robot = $[0.5, 1]$, Java Lin = $[0, 1]$ --> Java Lin wins $25\%$ of the time
    - Case Probabilities: $(0.5 \times 0.5) + (0.5 \times 0.25) = 0.375$
2) Case: $0.5 \le a \le 0.6125$ (probability $11.25\%$)
    - Spears Robot rethrows ($62.5\%$): Both are $[0, 1]$ --> Java Lin wins $50\%$ of the time
    - Spears robot keeps ($37.5\%$): Spears Robot = $[0.625, 1]$, Java Lin = $[0, 1]$ --> Java Lin wins $18.75\%$ of the time
    - Case Probabilities: $(.625 \times 0.5) + (0.375 \times 0.1875) = 0.3828125$
3) Case: $0.6125 \le a \le 1$ (probaility $38.75\%$)
    - Spears Robot rethrows ($62.5\%$): Spears Robot $[0, 1]$, Java Lin = $[0.6125, 1]$ --> Java Lin wins $80.625\%$ of the time
    - Spears Robot keeps ($37.5\%$): Spears Robot $[0.625, 1]$, Java Lin = $[0.6125, 1]$ --> Java Lin wins $\frac{15}{31} \approx 48.38\%$ of the time
    - Case Probabilties: $[0.625 \times 0.80625) + (0.375 \times \frac{15}{31}) = (\frac{129}{256}) + (\frac{45}{248}) = \frac{5439}{7936} \approx 0.6853$

$$
P(\text{Win}) = (0.5 \times 0.375) + (0.1125 \times 0.3828125) + (0.3875 \times \frac{5439}{7936})
$$
$$
P(\text{Win}) = (\frac{3}{16}) + (\frac{441}{10240}) + (\frac{5439}{20480}) = \frac{10161}{20480}
$$
$$
P(\text{Win}) = \frac{10161}{20480} \approx 0.49614257812 \approx 49.61\%
$$

{{< notice info >}}
The correct win probaility given all the new strategies should be $\frac{(229 - 60 \sqrt{5})}{192} \approx 0.4939370904 \approx 49.39\%$
{{< /notice >}}

# Validation through Simulation

To test these results simply ensure you have [Zig](https://ziglang.org/) installed on your machine then naviagte to this direcotry and run the following command:

```zig
zig build run
```