# clickup-git-hook

Effective engineers invest in tools to increase efficiency.

### Inspiration :- 
- Effective engineer book - https://blog.d46.us/effective-eng-summary/ , where they say "Effective engineers invest in tools to increase efficiency.", every second saved of team is golden.
- Pivotal Hook - https://github.com/jimothyGator/pivotal-git-hooks, the current ClickUp hook is not as comprehensive but I believe it should get 80% job done(Pareto Principle)
- Jira Hook - https://medium.com/@nicklee1/prepending-your-git-commit-messages-with-user-story-ids-3bfea00eab5a



Past(without this hook)
- You enable GitHub integration for your ClickUp space.
- You create a new branch for your clickup task.
- Now, when move onto making Git commits, you'll need to manually specify ClickUp task ID in commit msg something like `git commit -m "[#taskID] Commit msg"
- Pain point here is, every time you'll need to remember about task ID and make sure with every commit you're prepending it.
- Done, and now every commit and PR is tracked on ClickUp.

Future(with this hook)
- Same as in past.
- You create a new branch with "<task_id>_<meta>" where task_id is ID of task on ClickUp starting with "#" and meta is any free form text regarding this branch/feature/bug
- Now, when move onto making Git commits, you'll **need not to** manually specify ClickUp task ID, you can commit directly like `git commit -m "Commit msg" and this hook will figure out basis your the taskID specified in the branch what to prepend the commit with.
- Done, and now every commit and PR is tracked on ClickUp.


Note - Your ClickUp task ID should start with # and should atleast have 4 characters, it does not matter where this info is present in the branch.

## Steps to run
- Move old pre-commit file with `mv .git/hooks/prepare-commit-msg .git/hooks/prepare-commit-msg.old`(WARNING:- If you're using any old prepare-commit-hooks please take care of them)
- Open `.git/hooks/prepare-commit-msg` in your favorite editor from your project directory where git is initialized for this repo.
- Copy and paste content of "prepare-commit-msg" above file.
- Make it executable with "chmod + .git/hooks/prepare-commit-msg"
- Re-intialise your git with `git init` in project directory
- Enjoy 💥


## Going Global

Manually adding this hook to all your projects is boring and not very DRY. Luckily, applying this globally is easily done by modifying your global git configuration to use a template:

Please find steps below - 
- Firstly, create a git templates directory with - `mkdir -p ~/.git-templates`
- Set up a git template directory using the git config command - `git config --global init.templatedir '~/.git-templates' 
- Then create the hooks directory for global hooks in your template folder:- mkdir -p ~/.git-templates/hooks 
- Afterwards, copy your hooks into this newly created directory and ensure permissions are correctly set on the file with `chmod a+x ~/.git-templates/hooks/prepare-commit-msg`
- Done! Now whenever you run git commit, it will prepend the first segments of the branch to the commit message! 
- For existing projects, you just need to reinit the git directory (don’t worry, it won’t break anything!) by running the following in the project root directory: `git init`
- :boom:




