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
        Tôi là nghiên cứu sinh tiến sĩ ngành Kỹ thuật hệ thống cơ khí tại Khoa sau đại học Khoa học và Công nghệ Tiên tiến, Đại học Tokyo Denki. Với tư cách nghiên cứu sinh học bổng SPRING, tôi đánh giá và cải tiến bộ đồ hỗ trợ lực nhằm giảm mệt mỏi cho người lao động lành nghề trên công trường. Chủ đề hiện tại là cách đánh giá góc khớp, thu bằng motion capture, theo hướng vừa nhìn thấy vừa định lượng.
      headings:
        about: 'Giới thiệu'
        education: 'Học vấn'
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
      title: 'Nghiên cứu'
      subtitle: ''
      text: |-
        Mục tiêu nghiên cứu của tôi là giảm gánh nặng thể chất khi duy trì hạ tầng và khi chăm sóc, những việc tăng lên cùng xã hội già hóa, bằng thiết bị hỗ trợ. Tôi tập trung vào công việc vẫn phụ thuộc sức người, như thi công điện, và vào việc đo bộ đồ hỗ trợ làm thay đổi tư thế và mệt mỏi ra sao.
    design:
      columns: '1'
  - block: markdown
    content:
      title: 'Khác'
      subtitle: ''
      text: |-
        Ngoài nghiên cứu, tôi cũng dựng và vận hành máy chủ, dùng đài vô tuyến nghiệp dư (FM 430 MHz và drone FPV 5,7 GHz), và năm 2023 đã phát hành ứng dụng iOS Kanji Pittan trên App Store.
    design:
      columns: '1'
  - block: collection
    id: publications
    content:
      title: Công bố gần đây
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
      title: Thuyết trình
      filters:
        folders:
          - events
    design:
      view: citation
  - block: collection
    id: news
    content:
      title: Tin tức
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
      view: date-title-summary
      spacing:
        padding: [0, 0, 0, 0]
---
