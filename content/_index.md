---
# Leave the homepage title empty to use the site title
title: ''
summary: ''
date: 2022-10-24
type: landing

design:
  # Default section spacing
  spacing: '6rem'

sections:
  - block: resume-biography-3
    content:
      # Choose a user profile to display (a folder name within `content/authors/`)
      username: me
      text: |
        　東京電機大学大学院 博士後期課程に在籍し、機械工学を専門として研究に従事。2025年4月より、東京電機大学SPRINGスカラシップ研究学生として採用される。現在は、建設業に従事する技能者の疲労軽減を目的としたパワーアシストスーツ（PAS）の評価および改良に取り組んでおり、視覚的かつ定量的な評価手法の開発を主たる研究テーマとしている。<br><br>
        　研究活動に加えて、個人にてサーバー環境の構築・運用を行っており、仮想化技術やWebサービスのホスティングを通じて、インフラ関連技術の習得にも注力している。2021年にはアマチュア無線局を開局し、430MHz帯におけるFM通信のほか、5.7GHz帯を用いたFPVドローンの運用にも携わっている。さらに、ソフトウェア開発にも関心を持ち、2023年にはiOS向けアプリケーション『漢字ぴったん』をApp Storeにて公開した。
      # Show a call-to-action button under your biography? (optional)
      # button:
      #   text: Download CV
      #   url: uploads/resume.pdf
      headings:
        about: ''
        education: ''
        interests: ''
    design:
      # Use the new Gradient Mesh which automatically adapts to the selected theme colors
      background:
        gradient_mesh:
          enable: true

      # Name heading sizing to accommodate long or short names
      name:
        size: md # Options: xs, sm, md, lg (default), xl

      # Avatar customization
      avatar:
        size: medium # Options: small (150px), medium (200px, default), large (320px), xl (400px), xxl (500px)
        shape: circle # Options: circle (default), square, rounded
  - block: markdown
    content:
      title: '📚 My Research'
      subtitle: ''
      text: |-
        　私の描く将来のキャリアは、少子高齢化に伴うインフラ人材の労働負荷及び介護負担増加の課題に取り組む研究者となることである。日本の公共インフラの維持に関しては近い将来、困難な状況になることが想定可能である。気候変動に伴う災害の増加や人口減少の課題に直面してきた日本が、世界に先駆けて革新的な対策としてPASを普及させることは有意義な挑戦に値すると私は考えている。
        
        　また、私はこれまでに高齢者及び障碍者の支援に関する研究にも取り組んできた。高齢化によって家庭の中でも身体的な負担の大きい仕事が増えている現代の日本にとってもPASは重要である。日本だけでなく、世界共通の課題に貢献できる研究を進めていきたい。
    design:
      columns: '1'
  # - block: collection
  #   id: papers
  #   content:
  #     title: Featured Publications
  #     filters:
  #       folders:
  #         - publication
  #       featured_only: true
  #   design:
  #     view: article-grid
  #     columns: 2
  - block: collection
    id: publications
    content:
      title: Recent Publications
      text: ''
      filters:
        folders:
          - publications
        exclude_featured: false
    design:
      view: citation
  - block: collection
    id: talks
    content:
      title: Recent & Upcoming Talks
      filters:
        folders:
          - events
    design:
      view: article-grid
  - block: collection
    id: news
    content:
      title: Recent News
      subtitle: ''
      text: ''
      # Page type to display. E.g. post, talk, publication...
      page_type: news
      # Choose how many pages you would like to display (0 = all pages)
      count: 5
      # Filter on criteria
      filters:
        author: ''
        category: ''
        tag: ''
        exclude_featured: false
        exclude_future: false
        exclude_past: false
        publication_type: ''
      # Choose how many pages you would like to offset by
      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      # Choose a layout view
      view: news
      # Reduce spacing
      spacing:
        padding: [0, 0, 0, 0]
  # - block: collection
  #   id: posts
  #   content:
  #     title: Recent posts
  #     subtitle: ''
  #     text: ''
  #     # Page type to display. E.g. post, talk, publication...
  #     page_type: blog
  #     # Choose how many pages you would like to display (0 = all pages)
  #     count: 5
  #     # Filter on criteria
  #     filters:
  #       author: ""
  #       category: ""
  #       tag: ""
  #       exclude_featured: false
  #       exclude_future: false
  #       exclude_past: false
  #       publication_type: ""
  #     # Choose how many pages you would like to offset by
  #     offset: 0
  #     # Page order: descending (desc) or ascending (asc) date.
  #     order: desc
  #   design:
  #     # Choose a layout view
  #     view: date-title-summary
  #     # Reduce spacing
  #     spacing:
  #       padding: [0, 0, 0, 0]
  # - block: cta-card
  #   demo: true # Only display this section in the HugoBlox Kit demo site
  #   content:
  #     title: 👉 Build your own academic website like this
  #     text: |-
  #       This site is generated by HugoBlox Kit - the FREE, Hugo-based open source website builder trusted by 250,000+ academics like you.

  #       <a class="github-button" href="https://github.com/HugoBlox/kit" data-color-scheme="no-preference: light; light: light; dark: dark;" data-icon="octicon-star" data-size="large" data-show-count="true" aria-label="Star HugoBlox/kit on GitHub">Star</a>

  #       Easily build anything with blocks - no-code required!

  #       From landing pages, second brains, and courses to academic resumés, conferences, and tech blogs.
  #     button:
  #       text: Get Started
  #       url: https://hugoblox.com/templates/
  #   design:
  #     card:
  #       # Card background color (CSS class)
  #       css_class: 'bg-primary-300 dark:bg-primary-700'
  #       css_style: ''
---
