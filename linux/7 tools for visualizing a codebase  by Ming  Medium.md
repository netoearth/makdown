Need to write a README file, but not sure what to say? If this is a frustration that bothers you frequently, you might consider beefing your document up with a diagram. After all, a picture is worth a thousand words, as the cliche goes.

![](https://miro.medium.com/max/700/0*w952tps00S4Jy1cf)

Photo by [Hanna Morris](https://unsplash.com/@hcmorr?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/diagram?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

This article collects tools that generates graphs for a code repository.

## Visualize files by size and type

Let’s **start with the most generic** tool, `[repo-visualizer](https://github.com/githubocto/repo-visualizer)`. It plots files as bubbles, indicating their extension names and sizes with colors and sizes, respectively. It's [brought to you](https://next.github.com/projects/repo-visualization/) by [GitHub Next](https://next.github.com/), a lab at GitHub the company, and (naturally) it's packaged as a [GitHub Action](https://github.com/features/actions).

## Visualize Docker Compose files

The next tool specifically caters to Docker users, but it’s still language-agnostic. To visualize `docker-compose.yml`, you can use `[docker-compose-viz](https://github.com/pmsipilot/docker-compose-viz)`:

```
docker run \--rm \-it \--name dcv \-v $(pwd):/input pmsipilot/docker-compose-viz render \-m image docker-compose.yml
```

Here’s how it would look:

![](https://miro.medium.com/max/417/0*yxLDD4lCKKvP-_Yt.png)

I like how it’s also plotting extra information like open ports and mounted volumes.

## Visualize [call graphs](https://en.wikipedia.org/wiki/Call_graph)

[Code2flow](https://github.com/scottrogowski/code2flow) supports a couple of **dynamic** languages, including Python, JavaScript, Ruby, and PHP.

Here’s the example provided in its README:

```
code2flow code2flow/engine.py code2flow/python.py --target-function=code2flow --downstream-depth=3
```

![](https://miro.medium.com/max/535/1*ley51O4jvxpkKqu11SHIQg.png)

Call graph of a student project by [Pamela Fox](https://twitter.com/pamelafox). [Slides](https://inst.eecs.berkeley.edu/~cs61a/sp22/assets/slides/30-Modularity.html#/17).

If **Python** is the only language you care about, you might have heard of `[pycallgraph](https://github.com/gak/pycallgraph)` [](https://github.com/gak/pycallgraph), but -- alas, the bane of open source software projects -- the original author had to abandon the project due to personal time constraints. The most sensible **alternative** I can find is `[pyan](https://github.com/davidfraser/pyan)`.

```
pyan *.py --uses --no-defines --colored --grouped --annotated --svg >myuses.svg
```

![](https://miro.medium.com/max/700/0*HLHpLcjzF0n8V9bI.png)

## Visualize dependencies

A fundamental functionality of build systems and package managers is dependency resolution. As you’d expect, many visualization tools tap into dependency graphs generated by these software to plot diagrams for a repository.

Under the hood, most of these tools use `graphviz` for the actual plotting work. Therefore, don't be surprised to discover that the diagrams share a similar style.

[Bazel](https://bazel.build/) is a language-agnostic build system. The developers behind **Bazel** know its users so well that they put up an [official guide](https://blog.bazel.build/2015/06/17/visualize-your-build.html) for visualizing dependencies defined with Bazel:

```
bazel query 'deps(//:main)' --output graph > dependencies.indot -Tpng < dependencies.in > dependencies.svg
```

It gives something like this:

![](https://miro.medium.com/max/201/0*f2OSom4CWV4X5dtD.png)

For **Python** packages in an environment, use `[pipdeptree](https://pypi.org/project/pipdeptree/)`:

```
pipdeptree --graph-output svg > dependencies.svg
```

![](https://miro.medium.com/max/700/0*Xm3JnqySRwwDitAq)

For **Java** projects built with [Maven](https://maven.apache.org/), `[depgraph-maven-plugin](https://github.com/ferstl/depgraph-maven-plugin)` is the way to go:

```
mvn com.github.ferstl:depgraph-maven-plugin:graph
```

![](https://miro.medium.com/max/700/0*JPLMYwrGpH-H0jPh.png)

## I want more interactivity!

Maybe you’re not here to fill up your README; rather, you just want to learn about a repo as quickly and intuitively as possible. If that’s the case, there are some nice tools you can play with:

-   [Gource](https://gource.io/): A locally-run software.
-   [CodeSee](https://www.codesee.io/): A cloud service that offers paid plans.

I’m not endorsing either of them, and they are beyond the scope of this post. Nevertheless, this serves as a good point to wrap up this post. Writing an ending is painful, and I’m sure you’re aware of that — Otherwise, you would not have landed on this very article that helps you evade the chore of composing words, would you?