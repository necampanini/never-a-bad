---
layout: page
title: Composition Vs. Aggregation - Part 2
---

I'd really like to cover more historical content before making a second post, but I feel I am beginning to understand composition and aggregation much more than I understood these topics a few weeks ago...Especially after harassing a coworker about dependency injection so much.

I feel more comfortable in my absence of knowledge pertaining to these topics simply because I am starting to see the physical (source code) differences between the two. Coupled with my very basic understanding of dependency in general, the overall question of 'Composition Vs Aggregation' starts to make more sense.

> ### *Disclaimer: The following post is probably entirely in the wrong, and this is mostly for my own amusement.*

While I have not come across historical analysis of these two subjects, I am going to go out on a limb, and say that Aggregation is the more modern construct. A few things are making me lean in this direction, here's one of them:

## Striving for loosely coupled designs.

This is an abstract design principle that I can hardly claim to fully comprehend. But if I am understanding my readings correctly, concrete class objects that instantiate other concrete objects within themselves, are *dependent* on that class. That is to say, one object's ability to be instantiated and function as expected, is directly impacted on the availability of that second object. I'll attempt to hack through a C# example of Composition Vs Aggregation concerning this design principle.

#### Composition

{% highlight c# %}
  //An electric guitar that makes no sense without strings/electronics
  public class CompositionGuitar
  {
    private final HumbuckerSet humbuckerSet;
    private final StringSet stringSet;

    public CompositionGuitar(Brand brand){
      humbuckerSet = new HumbuckerSet(brand);
      stringSet = new StringSet(brand);
    }

    public void Shred(){
      stringSet.DoubleTapping();
      humbuckerSet.Transmit();
    }
  }
{% endhighlight %}

In this example, the guitar is used as a whole, and only serves its purpose once *composed* of its parts. Slash did not get drunk and shred on stage missing all his strings and half the electronics.

#### Aggregation
{% highlight c# %}
//An electric guitar a hobbyist has assembled and derived use from at all stages. The strings and electronics exist and have worth outside of the guitar's assembly.

public class AggregationGuitar
{
  private HumbuckerSet humbuckerSet;
  private StringSet stringSet;

  void assemblePieces(HumbuckerSet humbuckerSet, StringSet stringSet)
  {
    this.humbuckerSet = humbuckerSet;
    this.stringSet = stringSet;
    Console.WriteLine("I enjoy assembling this instrument!");
  }

  public void Shred(){
    if (humbuckerSet != null && stringSet != null)
    {
      stringSet.SweepPick();
      humbuckerSet.Transmite();
      Console.WriteLine("This also has value!");
    }
  }
}
{% endhighlight %}

Here, the AggregationGuitar expects an already existing set of humbuckers and set of strings before it can call a method. It is not dependent on its creation, and the code will compile fine...I think.

### My reasoning so far:
Designs that more closely resemble collections of orthogonal objects just seem to be the more advanced topic to me than the alternative. It follows the loosely-coupled principle more closely and I'd be willing to wager that the concept of functional aggregation took time to formalize...

Perhaps I'm just talking out of my ass. I need to read more.
