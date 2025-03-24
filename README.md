Run it: ```apt install g++ geany libgmp-dev```. Open the .cpp in Geany.<br>
Append ```-lgmp``` to Geany's compile & build commands. Hit F9 once. F5 to run.

<br>

<p align="center">
  <img src="https://raw.githubusercontent.com/compromise-evident/prime-gap-RNG/refs/heads/main/Other/Terminal.png">
</p>

<br>
<br>

# How it works

<p align="center">
  <img src="https://raw.githubusercontent.com/compromise-evident/prime-gap-RNG/refs/heads/main/Other/Formula.png">
</p>

When a random file is dropped/entered as input,
a "private_seeds" file is created, which contains
an n-digit value (whose length you can set via "digit_length".)

That value is loaded and adjusted so that it is prime.
Now, the idea is to find prime gaps following the value,
and compare them to the average prime gap near that value.

If a gap is greater than the average gap, you get a 1 bit, else a 0 bit.
But this REPRODUCIBLY gets you many more 0 bits than 1 bits,
because the average gap is too large. Such an
occurrence is unacceptable for randomness.

And so the average gap is enhanced.
Using the formula above, a gap is then instead
compared to a fraction of the average gap.

As a result, not only do bits 1 & 0 occur nearly equally,
but so do all 256 bytes, as this tool demonstrates.

The formula is equivalent to: ```int enhanced_average_gap = ((average_gap * 44) / 63);``` <br>
Just put ```a/2 + a/7 + a/18``` in WolframAlpha.

The same process (randomness of continued gaps) is used
to update the "private_seeds" file with a new n-digit value.
You may alter this value within that file, at any time
(introducing additional sources of randomness.)

After each run, an "analysis" file is generated.
It contains bit & byte occurrence, distinct bytes,
total bytes, all the bytes raw, and all the
text bytes for visual.
