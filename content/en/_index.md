---
title: ''
summary: ''
date: 2022-10-24
type: landing

design:
  spacing: '4rem'

sections:
  - block: resume-biography-3
    content:
      username: me
      text: |
        I am a Ph.D. student in Mechanical Systems Engineering at the Graduate School of Advanced Science and Technology, Tokyo Denki University. As a SPRING Scholarship Research Student, I evaluate and improve power assist suits that reduce fatigue for skilled workers on construction sites. My current topic is a visual and quantitative way to evaluate joint angles captured by motion capture.
      headings:
        about: 'About'
        education: 'Education'
        interests: ''
    design:
      background:
        gradient_mesh:
          enable: true
      name:
        size: md
      avatar:
        size: medium
        shape: circle
  - block: markdown
    content:
      title: 'Research'
      subtitle: ''
      text: |-
        My research aim is to reduce the physical load of maintaining infrastructure and of caregiving, both of which grow with an aging society, by using assistive devices. I focus on work that still depends on human labor, such as electrical construction, and on measuring how an assist suit changes posture and fatigue.
    design:
      columns: '1'
  - block: markdown
    content:
      title: 'Other'
      subtitle: ''
      text: |-
        On my own I also build and run servers, operate an amateur radio station (430 MHz FM and 5.7 GHz FPV drones), and released an iOS app, Kanji Pittan, on the App Store in 2023.
    design:
      columns: '1'
  - block: collection
    id: publications
    content:
      title: Recent publications
      text: ''
      count: 5
      filters:
        folders:
          - publications
        exclude_featured: false
    design:
      view: citation
  - block: collection
    id: talks
    content:
      title: Talks
      filters:
        folders:
          - events
    design:
      view: article-grid
  - block: collection
    id: news
    content:
      title: News
      subtitle: ''
      text: ''
      page_type: news
      count: 5
      filters:
        author: ''
        category: ''
        tag: ''
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ''
      offset: 0
      order: desc
    design:
      view: news
      spacing:
        padding: [0, 0, 0, 0]
---
