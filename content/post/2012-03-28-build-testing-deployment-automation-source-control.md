---
title: 'Build, Testing & Deployment Automation: Source Control'
author: jbeckham
layout: post
date: 2012-03-28
url: /2012/03/build-testing-deployment-automation-source-control/
categories:
  - Build Automation
  - Dev
tags:
  - SVN
---
Here's an old post I just found that I had started a long time ago but apparently never finished. Posting as is&#8230;

&nbsp;

We use SVN for our versioning, and TortoiseSVN on the client.

Since there is only one person working on the project, we've opted for a simple version control strategy. We use a simplified <a href="http://blogs.collab.net/subversion/2007/11/branching-strat/" target="_blank">stable trunk</a> strategy and release from /trunk. The goal is to keep /trunk releasable at any given moment. All development is done against a long-lived branch: /branches/_dev. When a feature is done (tested, documented, etc), it is merged to /trunk. Here is the complete process with each piece explained below:

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="svn-process" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/svn-process_thumb.png?resize=694%2C324" alt="svn-process" border="0" data-recalc-dims="1" />][1]

&nbsp;

Feature development is done against the development branch:

&nbsp;

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="devbranch" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/devbranch_thumb.png?resize=265%2C88" alt="devbranch" border="0" data-recalc-dims="1" />][2]

&nbsp;

When a feature is done, it is merged into the trunk

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="devmergedtotrunk" src="http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/devmergedtotrunk_thumb.png?resize=225%2C135" alt="devmergedtotrunk" border="0" data-recalc-dims="1" />][3]

If a feature is partially completed and a different story or bugfix needs to be worked on, the partially completed feature is shelved to a branch (/branches/<username>-<story number>. Once the other work has been completed and checked in, the shelved branch is merged back in with the developer's working copy of the development branch.

&nbsp;

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="shelved" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/shelved_thumb.png?resize=240%2C153" alt="shelved" border="0" data-recalc-dims="1" />][4]

When we are ready to release, we the latest revision in /trunk and tag it.

&nbsp;

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="releasetagged" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/releasetagged_thumb.png?resize=274%2C154" alt="releasetagged" border="0" data-recalc-dims="1" />][5]

&nbsp;

If we find a bug in production that must be fixed immediately, we create a new branch from the last release tag (which means that we're branching what we're currently running in production) and call it /branches/hotfix-<hotfix story #>. We deploy to staging from the hotfix branch to verify that the hotfix worked, and then deploy to production from the hotfix branch. Once everything is confirmed to be working, the hotfix branch is tagged then removed.

&nbsp;

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="hotfix" src="http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/hotfix_thumb.png?resize=463%2C132" alt="hotfix" border="0" data-recalc-dims="1" />][6]

&nbsp;

Also, once the hotfix is confirmed to be working, it is merged back into the other branches (/trunk and /dev)

[<img style="background-image: none; padding-left: 0px; padding-right: 0px; display: inline; padding-top: 0px; border-width: 0px;" title="hotfix-merged" src="http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/hotfix-merged_thumb.png?resize=251%2C260" alt="hotfix-merged" border="0" data-recalc-dims="1" />][7]

 [1]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/svn-process.png
 [2]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/devbranch.png
 [3]: http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/devmergedtotrunk.png
 [4]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/shelved.png
 [5]: http://i0.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/releasetagged.png
 [6]: http://i1.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/hotfix.png
 [7]: http://i2.wp.com/www.joelbeckham.com/wp-content/uploads/2012/03/hotfix-merged.png