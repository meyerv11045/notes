

## Circle-Rectangle Intersection Detection

- [Stack Overflow](https://stackoverflow.com/questions/401847/circle-rectangle-collision-detection-intersection)

### Axis-Aligned Rectangle

``` python
def intersects(circle: Circle, rect: Rect) -> bool:
    circle_dist_x = abs(circle.x - rect.x)
    circle_dist_y = abs(circle.y - rect.y)

    if (circle_dist_x > (rect.width / 2 + circle.r) or
        circle_dist_y > (rect.height/ 2 + circle.r)):
        return False

    if (circle_dist_x <= (rect.width/2) or
        circle_dist_y <= (rect.height/2)):
        return True

    corner_dist_sq = (circle_dist_x - rect.width / 2)**2 + (circle_dist_y - rect.height / 2)**2

    return corner_dist_sq <= circle.r**2
```

## Point in Convex Polygon

- [Stack Overflow](https://stackoverflow.com/questions/2752725/finding-whether-a-point-lies-inside-a-rectangle-or-not)
- Let edges be oriented counterclockwise 
- For each edge of polygon, if the point lies to the left of the edge, it is in the polygon 