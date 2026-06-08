# Hackerland Radio Transmitters

I had to look up the solution for this one after some failed attempts

I was overcomplicating it thinking that greedy search would not work, but you just place the first transmitter as far right as possible (but still covering the first house), go to the next uncovered house, and repeat

Much simpler than it was in my head.

``` python
def hackerlandRadioTransmitters(x, k):
    houses = sorted(set(x))
    count = 0
    i = 0
    n = len(houses)

    while i < n:
        # houses[i] is the leftmost uncovered house
        # find the rightmost house within range k of it - place transmitter there
        start = houses[i]
        i += 1
        while i < n and houses[i] <= start + k:
            i += 1
        # houses[i-1] is the transmitter location
        transmitter = houses[i - 1]
        count += 1

        # skip all houses covered by this transmitter (up to transmitter + k)
        while i < n and houses[i] <= transmitter + k:
            i += 1

    return count
```