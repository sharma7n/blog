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

We are tasked with writing a program to score a hypothetical game of darts. The scoring system has the following rules:

- The player is allowed to throw as many darts as they want, but the game stops once they miss three (total) throws.
- Missed throws are awarded no points.

Consider the following python code:

```python
import collections


def score(shots):
    points_by_zone = collections.defaultdict(collections.Counter)
    misses = 0
    penalty = 0

    for shot in shots:
        if misses >= 3:
            break
    
        if shot.zone == 'easy':
            points_by_zone['easy'][shot.points] += 1
        elif shot.zone == 'hard':
            points_by_zone['big'][shot.points] += 1
        elif shot.zone == 'penalty':
            penalty += 1
        else:
            misses += 1
  
    return {
        'points_by_zone': points_by_zone,
        'penalty': penalty,
        'misses': misses,
    }
```