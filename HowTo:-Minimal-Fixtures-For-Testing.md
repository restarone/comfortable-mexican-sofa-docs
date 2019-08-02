Your tests may hit the home page of your site now and again, and having a stubbed out page in CMS will make it easy.

test/fixtures/comfy/cms/sites.yml

    main:
      label: main
      identifier: main
      hostname: www.example.com
      path:
      locale: en

test/fixtures/comfy/cms/pages.yml

    root:
      site: main
      label: Home
      full_path: /

With just these two files, your tests can how bring up the root URL without error.  Of course, if you're using helpers and dynamic sections in your pages you probably want to bring in a full test page for testing.