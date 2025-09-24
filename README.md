# Important

As of September 24th, 2025, this repository will be deprecated. For future updates, please refer to the repository on the official Huawei Cloud Latam organization: <b><a href="https://github.com/huaweicloud-latam/knowledge-base">repository</a></b>.

# huaweicloud-knowledge-base

This repository is home to a collaborative, public knowledge base website for Huawei Cloud services. In this knowledge base, you can find technical guides for specific scenarios. You can access the website in the following hyperlink: <a href="https://hatz-d.github.io/huaweicloud-knowledge-base/">website</a>, available in English and Portuguese. Use the search bar or the navigation menu to browse the knowledge base.

## How you can contribute

In order to contribute to the knowledge base, you may <b><a href="https://github.com/Hatz-D/huaweicloud-knowledge-base/fork">fork this repository</a></b> and submit a pull request containing the desired documentation in the markdown file format and its assets. After having forked the repository, go to the <code>Pages</code> section and enable GitHub pages. After that, go to the <code>Actions</code> section, enable the workflows and manually run the workflow <code>Deploy Jekyll site to Pages</code> in order to build and deploy the knowledge center website. After the workflow has been successfully completed, you may access the website.

## Repository structure

This repository is structured as follows:

<ul>
  <li><code>/docs</code>: directory in which the documentations are stored. In this directory, upload the desired documentation following the structure <code>/docs/{service-category}/{service-name}/{documentation-name}.md</code>. If the documentation is written in Portuguese, modify the file suffix to <code>.pt.md</code>.</li>
  <li><code>/assets/images</code>: directory in which the images of the documentations are stored. In this directory, upload the documentation assets following the structure <code>/assets/images/{service-category}/{service-name}/{documentation-name}/{assets}</code></li>
</ul>

You may refer to the documentations present in this repository as examples.

### Documents Headers

All the documentations <b>must</b> have the following header for proper indexing:

```shell
---
title: {documentation title}
layout: default
parent: {HWC service name} ({HWC service name abbreviation})
grand_parent: {HWC service category}
permalink: /docs/{HWC service category}/{HWC service name abbreviation}/{documentation title}
lang: pt {only when applicable}
---
```

Example (English):

```shell
---
title: Migrating K8S Cluster Using Velero
layout: default
parent: Cloud Container Engine (CCE)
grand_parent: Containers
permalink: /docs/containers/cce/migrating-k8s-cluster-using-velero
---
```

Example (Portuguese):

```shell
---
title: Migrando Cluster K8S Usando Velero
layout: default
parent: Cloud Container Engine (CCE)
grand_parent: Containers
lang: pt
permalink: /docs/containers/cce/migrating-k8s-cluster-using-velero
```

### Tutorial Video

TODO

## Licensing and Attribution

This repository is licensed under the [MIT License]. You are generally free to reuse or extend upon this code as you see fit; just include the original copy of the license (which is preserved when you "make a template"). While it's not necessary, we'd love to hear from you if you do use this template, and how we can improve it for future use!

The deployment GitHub Actions workflow is heavily based on GitHub's mixed-party [starter workflows]. A copy of their MIT License is available in [actions/starter-workflows].

----

[^1]: [It can take up to 10 minutes for changes to your site to publish after you push the changes to GitHub](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site).

[Jekyll]: https://jekyllrb.com
[Just the Docs]: https://just-the-docs.github.io/just-the-docs/
[GitHub Pages]: https://docs.github.com/en/pages
[GitHub Pages / Actions workflow]: https://github.blog/changelog/2022-07-27-github-pages-custom-github-actions-workflows-beta/
[Bundler]: https://bundler.io
[use this template]: https://github.com/just-the-docs/just-the-docs-template/generate
[`jekyll-default-layout`]: https://github.com/benbalter/jekyll-default-layout
[`jekyll-seo-tag`]: https://jekyll.github.io/jekyll-seo-tag
[MIT License]: https://en.wikipedia.org/wiki/MIT_License
[starter workflows]: https://github.com/actions/starter-workflows/blob/main/pages/jekyll.yml
[actions/starter-workflows]: https://github.com/actions/starter-workflows/blob/main/LICENSE
