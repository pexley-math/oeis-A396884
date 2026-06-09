# How many smallest polyiamonds contain every n-iamond?

*Peter Exley, Independent Researcher, Brisbane, Australia. Submitted: Jun 09 2026.*

A polyiamond is a shape made of unit triangles joined edge to edge. Fix a size n
and look at every n-iamond at once. Some larger shapes are big enough to hold a
copy of all of them. Among those universal shapes, the smallest are the most
economical. We count how many different ones exist.

## The problem

For each n we consider the free n-iamonds: the distinct shapes of n unit
triangles, where two shapes are the same if one is a rotation or reflection of
the other. A connected polyiamond C is a container for size n if every free
n-iamond fits inside C as a sub-shape under the symmetries of the triangular
lattice. Let k(n) be the fewest triangles any container needs; this is the
companion sequence A392363. We count the containers that achieve this minimum:
a(n) is the number of distinct connected polyiamonds of size k(n) that contain
every free n-iamond, where two containers are the same when one is a rotation,
reflection, or lattice translation of the other.

This is the triangular-lattice analog of the square-lattice count A352029.

The listed values are the number of minimum-size containers found within a
finite search window whose width equals n (forced by the straight n-iamond) and
whose height grows as `max(4, (n+2)//3)`; global minimality over all bounding
boxes is conjectured but not separately certified.

## Definitions

A *free n-iamond* is one of the A000577(n) shapes of n unit triangles, counted
up to rotation and reflection. A *container* for size n is a connected
polyiamond that contains a copy of every free n-iamond. The *container size*
k(n) is the least number of triangles in any container. A container is *minimal*
when it has exactly k(n) triangles. We count minimal containers up to the
rotations, reflections, and translations of the triangular lattice; a(n) is that
count.

## The values

**Result.** The number of minimal polyiamond containers is

| n | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| a(n) | 1 | 1 | 1 | 1 | 4 | 5 | 39 | 13 | 26 |

with corresponding minimum container sizes k(n) = 1, 2, 3, 5, 7, 10, 13, 16, 19.
For n from 1 to 4 there is a single minimal container; the count first branches
at n = 5. The shapes of the minimal containers are drawn in the gallery
[`figures.pdf`](figures.pdf). As n grows the containers grow compact and
roughly triangular, packing the longest and widest n-iamonds into the fewest
shared cells.

## How we know

We compute a(n) in two halves. First we fix the size k(n) and ask a constraint
solver to find every connected arrangement of k(n) triangles that holds all free
n-iamonds, reporting one representative of each shape up to symmetry. A CDCL
satisfiability solver enumerates these arrangements exhaustively: it reports a
container, we forbid that shape and all of its symmetric copies, and we repeat
until none remain. Second, we confirm the size k(n) is truly minimal by proving
that no container of size k(n) - 1 exists.

Two independent checks confirm each value. A separate program, sharing no code
with the solver, independently determines the count by a direct geometric search and agrees on
every term it can reach. The minimality of k(n) is backed by a machine-checked
proof certificate that no smaller container exists. The two halves -- the count
at size k(n) and the proof that nothing smaller works -- together pin down a(n).

## Patterns and open questions

The sequence is strikingly non-monotonic. It climbs to a(7) = 39, falls to
a(8) = 13, and rises again to a(9) = 26. This is not an artifact: the
square-lattice analog A352029 swings the same way, reaching 204 at n = 7 before
collapsing to 7 at n = 8. A jump in the forced size k(n) can sharply cut the
number of distinct minimal containers, because a larger required size admits
fewer shapes that are at once minimal and universal.

We found no closed form or low-order recurrence that fits the nine known terms, and the non-monotonic jumps make a simple polynomial unlikely. We searched the
OEIS for the sequence and its standard transforms and found no match, so the
sequence is new. The value a(9) is the current frontier: at n = 10 the
enumeration grows beyond a practical time budget.

We leave open whether a(n) admits any closed form, how it grows, and whether the
within-window minimality proved here can be promoted to global minimality for
all n.

## Further reading

This work was inspired by the OEIS and the community of contributors who maintain
it.

- Mason, J. (2022). "A352029: a(n) is the number of minimalist polyominoes that can contain all n-ominoes." The On-Line Encyclopedia of Integer Sequences. https://oeis.org/A352029
- Sloane, N. J. A. "A000577: Number of triangular polyominoes (or polyiamonds) with n cells." The On-Line Encyclopedia of Integer Sequences. https://oeis.org/A000577
- Exley, P. (2026). "A392363: Smallest connected polyiamond containing all free n-iamonds." The On-Line Encyclopedia of Integer Sequences. https://oeis.org/A392363

## License

[CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/) -- see `LICENSE`. This work is freely available; a citation or acknowledgment is appreciated but not required.
