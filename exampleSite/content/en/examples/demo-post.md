---
title: "Demo Post: With a long enough subtitle to use two lines"
date: 2021-11-23T00:11:54-05:00
author: false
summary: "A demo post for [Dananke](/)"
tags:
  - examples
---

Just to make sure the site works[^1] and audit check doesn't fail when there is content with the audit check.

   ```bash
   #!/bin/bash
   set -o pipefail
   
   HUGO_BUILD_URL="$1"
   
   # Should only occur using Netlify CLI
   if [ -z "HUGO_BUILD_URL" ]
   then
       HUGO_BUILD_URL="https://www.example.com/"
   fi
   
   shift
   
   ( set -o pipefail && cd themes/hugo-geekdoc && npm install --no-save && npx gulp default )
   
   HUGO_MINIFY_TDEWOLFF_HTML_KEEPCOMMENTS=true HUGO_ENABLEMISSINGTRANSLATIONPLACEHOLDERS=true hugo ${HUGO_BUILD_URL:+-b $HUGO_BUILD_URL} && grep -inorE "<\!-- raw HTML omitted -->|ZgotmplZ|hahahugo|\[i18n\]|\(<nil>\)" public/; RET="$?"
   
   if [ "$RET" != "0" ]
   then
       hugo --gc ${HUGO_BUILD_URL:+-b $HUGO_BUILD_URL} --cleanDestinationDir "$@"; RET=$?
   else
       cd ..
   fi
   
   exit "$RET"
   ```

[^1]: But let's also throw a footnote in here too, so that the html validator
      doesn't complain about our 'relaxing' (to specification instead of stricter!)
      the CSS `id` check when there are not any `id`s that need that loosening. I
      really need to report this upstream…
