---
{
  "type": "blog",
  "author": "Nik Sharma",
  "title": "Switch on Type vs Polymorphism",
  "description": "Conventional wisdom tells us to prefer polymorphism over switch statements, but sometimes this is wrong.",
  "image": "/images/icon-png.png",
  "published": "2020-03-07",
  "draft": true,
}
---

_Conventional wisdom tells us to prefer polymorphism over switch statements, but sometimes this is wrong._

Points:
- c2 wiki: https://wiki.c2.com/?ReplaceConditionalWithPolymorphism; https://wiki.c2.com/?SwitchStatementsSmell
- Anti-If Campaign: https://francescocirillo.com/pages/anti-if-campaign
- Uncle Bob: https://blog.cleancoder.com/uncle-bob/2019/06/16/ObjectsAndDataStructures.html
- Polymorphism in OO languages
- Exhaustive Sum Types in static FP languages
- Code snippets / personal experience

Consider the following python code:

```python
import collections


def total_score(games):
    state = collections.defaultdict(list)
    misses = 0
    penalty = 0

    for game in games:
        if misses >= 3:
            break
    
        if game.reward == 'small':
            state['small'].append(game)
        elif game.reward == 'big':
            state['big'].append(game)
        elif game.reward == 'penalty':
            penalty += 1
        else:
            misses += 1
  
    small_score = sum(g.score for g in state['small'])
    big_score = sum(g.score for g in state['big'])
    return small_score + (2 * big_score) - penalty
```