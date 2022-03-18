## A GitHub Learning Lab Introduction to Continous Integration Cliff Notes

Because there are bugs in this one

#

## **Each step is covered. I've tried not giving any information that isn't necessary to avoid an inescapable dead end due to github-learning-lab bot errors in this one. [My completed public repo can be found here](https://github.com/dkoch84/github-actions-for-ci) if you find you need a little extra help. If you are still puzzled at any point, reach out to me. Just shoot me a link to your repo and say hello.**

#

### **1. Complete as directed**

### **2. After making the PR, the bot's responses may be found in the wrong tab (Files Changed vs Conversation). Resolve the comments to move forward, no matter where they are found.**

<p align="center">
  <img src=images/step2.png />
</p>

### **3. Working in PR "CI for Node" - Complete as directed**

### **4. Working in PR "CI for Node" - Complete as directed**

### **5. Working in PR "CI for Node" - Complete as directed, "Commit suggestion"**

<p align="center">
  <img src=images/step5.png />
</p>

### **6. Doesn't seem to exist. Complete the PR in step 5 then Step 7 is next. Issue is "A workflow for the entire team"**

### **7. Working in Issue "A workflow for the entire team" - Complete as directed**

### **8. Working in PR "Improve CI" - Complete as directed, "Commit suggestion"**

<p align="center">
  <img src=images/step8.png />
</p>

### **9. Working in PR "Improve CI" - There are changes made here that are not discussed. For example, the trigger condition is changed.**

One look at the diff between what you currently have and what the bot expects you to have afterwards tells you something isn't right.

<p align="center">
  <img src=images/step9-diff.png />
</p>

Expand the "**If you'd like to copy and paste the full workflow file...**" section and do that. Your worflow should now look like this:

```yaml
name: Node CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: npm install and build webpack
        run: |
          npm install
          npm run build

  test:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        os: [ubuntu-latest, windows-2016]
        node-version: [12.x, 14.x]

    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}
      - name: npm install, and test
        run: |
          npm install
          npm test
        env:
          CI: true
```

Commit this to your branch.

10. **Wait for the Action to complete and the bot to comment in the PR.**
11. **Working in PR "Improve CI"**

The bot wants you to make some changes. The bot is very wrong.

<p align="center">
  <img src=images/step11.png />
</p>

If you took the bot's suggestion here, you will delete your `build` task keyword and future steps will compound the error. Look at this diff and make this edit instead, we are simply adding the action as a 2nd step under already existing one.

<p align="center">
  <img src=images/step11-diff.png />
</p>

12. **Working in PR "Improve CI" - More bot errors.**

The first suggestion it has is to add a dependency on the **build** job to the **build** job. That just doesn't make sense. It wants to replace our instruction to use a particular build machine too. Not great. Line 8? Try line 22.

<p align="center">
  <img src=images/step12.png />
</p>

The second suggested change is also all wrong. See the diff instead

<p align="center">
  <img src=images/step12-diff.png />
</p>

13. **Working in PR "Improve CI" - Merge it**

<p align="center">
  <img src=images/step13.png />
</p>
14. __Working in PR "A custom workflow" - Complete as instructed__
15. __Working in PR "A custom workflow" - Commit the suggestion__
16. __Working in PR "A custom workflow" - Commit the suggestion__
17. __Working in PR "A custom workflow" - Follow instructions.__
18. __Working in PR "A custom workflow" - Follow instructions.__
