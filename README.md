If deploying to Netlify, you have to run a hugo build command first, despite Netlify ostensibly doing the build for you.

Go to the blog root and run `hugo -d output/`.

If there's an issue building, go into the themes/hugo-casper-two directory and run 
`git submodule update --init`

For tracking - you'll need to add the tracjer JS into the partials folder inside the theme folder.
I shoudl really fork that git submodule but for now just rmember to add it back in whenever you hav to repull the submodule.