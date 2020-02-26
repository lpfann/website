---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Decentralized Website"
subtitle: "How to host a personal website on IPFS"

summary: "This article explains how to turn a personal website into a decentralized site based on IPFS, Hugo and GitHub Actions."
authors: [admin]
tags: ["IPFS","Hugo","Textile","GitHub Actions","Automatic Deployment","Cloudflare DNS"]
categories: ["Decentralized Web"]
date: 2020-02-25T18:11:19+01:00
lastmod: 2020-02-25T18:11:19+01:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: "Image courtesy of [ipfs.io](https://ipfs.io), [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/)"
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
The website you are reading can be completely used without a running backend on a server.
Such a website is known as _static_.

_Static_ websites deliver all the content and logic (JavaScript) to the browser.
All the interaction, such as search or clicking on internal links, is happening through the JS scripts included.
While this sounds like a layman would expect it to, this is far from the current state of the internet.

In the early days, many websites only consisted of static HTML sites.
Today, many modern websites rely on a running centralized backend server.
This enables dynamic experiences but also leads to [link rot](https://en.wikipedia.org/wiki/Link_rot), where specific websites (and their URLs) have a limited lifespan.
Many people experienced the sight of dead links at least once and this problem is expected to grow with an ageing internet.

## Content-Addressable Storage

A recent push to decentralize the internet again lead to technologies such as content-addressable storage.

Normal URLs on the internet such as `https://lpfann.me/` are arbitrarily chosen words and have no relation to the actual content.

Content-addressing uses a mathematical hash function to _compress_ the contents of a website into a short string called a _hash_.
The great thing about hash functions is that they most likely produce a unique output and as such a unique address.

This allows use cases where people can serve and exchange content just based on a content hash.
An example for an application of this is [IPFS](https://ipfs.io) (Interplanetary Filesystem).

IPFS introduced an address scheme for content and also the exchange of information using peer to peer networking without a central server.
People using the IPFS application automatically act as servers for other peers when they have information another node needs.

This enables a more robust and decentralized web without the need of a big central server or a content distribution network.

To host a website using IPFS we need it to be static.

## Making a website static

This website is built using [Hugo](https://gohugo.io/) which already produces static output.
It is only important to enable [relativeURLs](https://gohugo.io/content-management/urls/#relative-urls) to work with the IPFS addressing.

We are also using the [Academic](https://sourcethemes.com/academic/) theme for Hugo.
Academic uses several external font and JavaScript resources to enhance the content presentation.
While hosting a IPFS-website with references to non-IPFS resources is perfectly possible, it is not completely decentralized.

Luckily the Academic theme also provides a [downloader tool](https://github.com/sourcethemes/academic-admin/), which saves all external assets inside the website folder. 

At the time of writing the main downloader does not support all assets yet, but an open [pull request](https://github.com/sourcethemes/academic-admin/pull/57) added support for most of the missing things.
Another thing missing were the fonts, which originally came from [Googles Font CDN](https://fonts.google.com/) which we downloaded manually.

Now we have a complete website running on local fonts and JavaScript assets[^1].
As such you could download the website files and kill the internet connection and you would have the same experience.

## Hosting an IPFS website

If we would use IPFS to hash our website we would get a content hash like this:

```sh
/ipfs/QmSPZuY3K1XieH7M9zh4qs9MEGFf4GZdBv3STaiJpBaC6o
```
Now somebody else could retrieve the website using his own IPFS client directly or using one of the available browser plugins.

{{< figure src="terminal_pin.png" title="Draft of this blog post hashed and pinned to local IPFS node." lightbox="true" >}}

For somebody else to retrieve the files of the website we would have to keep a IPFS node running or ask somebody else to keep it cached (_pinned_).

There are so called pinning services (e.g. [Pinata](https://pinata.cloud/)) which provide this service.
Another project is [Filecoin](https://filecoin.io/) which is built on top of IPFS.
It provides monetary incentive using a type of Blockchain to reward nodes to keep IPFS files pinned.

{{< tweet 1231996985760051200>}}
In the last few days we looked for ways to automatically pin this website when new content is added to the [git repository](https://github.com/lpfann/website).
Just yesterday [Textile](https://blog.textile.io/first-look-at-textile-buckets-dynamic-ipfs-folders/) announced dynamic _buckets_ working on top of IPFS.
While not the main focus of their blogpost, they also presented new GitHub Actions which automatically deploy content to their free bucket hosting.
We extended [their scripts](https://github.com/textileio/gatsby-ipfs-blog) on the demo site based on Gatsby to work with Hugo.
{{< figure src="gh-action.png" title="GitHub Action building and pushing files to Textile bucket" lightbox="true" >}}
Now after every push and pull request, the GitHub Action compiles Hugo output and pushes it to a Textile bucket which is also pinned and works with IPFS.

Our website content is automatically available under a content hash after every change and [push](https://github.com/lpfann/website/blob/master/.github/workflows/bucket_publish.yml) to the repository.


### DNS

To let people know that a site is available with IPFS one can use [DNSLinks](https://docs.ipfs.io/guides/concepts/dnslink/).
These are TXT records attached to DNS domains which hint at the IPFS resource available.
IPFS browser extensions can detect these records and automatically use IPFS for content retrieval when coming to such a site.

The scripts from Textile also included an [updater](https://github.com/lpfann/website/blob/master/.github/workflows/update_dnslink.yml) for DNS records which post the IPFS hash to Cloudflare DNS service.
This script updates the DNSLink after every manual release.

### Ethereum Name Service (ENS)

To have a completely decentralized solution one can use technologies like [ENS](https://ens.domains/) which is an alternative to the DNS system.

Our website is also available under the ENS domain [https://pfannschmidt.eth](https://pfannschmidt.eth) or via the transition link [https://pfannschmidt.eth.link/](https://pfannschmidt.eth.link) which uses the `eth.link` service to allow browsers without ENS support to visit the site.

For now, we update the IPFS hash stored in ENS manually, but we could automate this in the future. 

## Backwards Compatibility.

IPFS is still in its early stages.
Most popular browsers do not support the protocol which is necessary to reach the majority of web users.

Until that changes one additionally needs to host websites the traditional way using web servers and DNS.
One can use [Cloudflares](https://developers.cloudflare.com/distributed-web/ipfs-gateway/connecting-website/) IPFS gateway and DNS solution to automatically serve IPFS content over normal HTTP.

For now this Blog is hosted by [Netlify](https://www.netlify.com/) for non-IPFS enabled visitors.

## Summary

Overall this process is still very much a complicated and hard thing.
While IPFS and its ecosystem is steadily improving there is still a lot to do.

Luckily new services such as [Terminal.co](https://terminal.co/) are coming up which provide end to end decentralized hosting solutions.

[^1]: We have one[^2] external reference left which provides our visitor counting script. Missing it would not influence the usability negatively for the visitors. (You could argue it would improve the experience :wink:)
[^2]: After publishing this article we added a new [commenting system](https://commento.io/). While it is self hosted, it is not decentralized. Apparently, that is [still a non-trivial thing](https://fixingtao.com/2016/06/how-to-create-a-fairly-decentralized-commenting-system/) to do.