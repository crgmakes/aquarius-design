# Contributing
So you would like to contribute to the project? That is awesome! Here's how to get started:

## Getting Set Up

Go no further until you follow the [quick start guide](getting_start_md).

## Documentation

All text documentation is written in Markdown -- check out about markdown syntax [here](https://www.markdownguide.org/basic-syntax/).

## Making a Contribution

The Aquarius Github repo operates under a feature-branch methodology. This means that work for an enhancement or defect happens in a **separate branch** made specifically for that change (or series of changes). Individual contributors make changes in their forks, and merge them into the main repo's feature branch. Once the feature branch is done, it's then merged into master. After the merge, the resultant commit is tagged with a new release number. A description of this git methodology can be found [here](https://blog.scottlowe.org/2015/01/27/using-fork-branch-git-workflow/).

<!-- ## Locking
When working with text, git does an excellent job handling merging two separate versions of a file. However, we are using git to track CAD files where a merge process is much less simple. To solve this issue, we use Git LFS (Large File Storage).

Git LFS is a tool for tracking and managing large binary files using git. We use it mainly for the `lock` feature it provides. Merging KiCAD and FreeCAD files is technically possible given that they're stored in plaintext, but completely infeasible. To prevent the need to merge them, we instead have one person lock the source file before starting editing and until after merging so no conflicts arise.

The ability to lock files is unfortunately only available to accounts that have been given Collaborator credentials. Instead of locking files yourself, have a Collaborator lock them in your stead. If you haven't already, join the [Discord Server](https://discord.gg/z89v73tU) and ask about getting files locked in the #hardware channel. If you do have Collaborator status on Github, you can lock individual files with `git lfs lock FILENAME --remote upstream` where "upstream" is the name of the remote for the official Aquarius repo, not your own fork. Locking your own fork doesn't show up for others, so be sure to lock the official repo. There's also a script in the root directory of the repo called `lfs.sh` that helps with bulk locking files. Run the script without arguments to see usage instructions. When running the script, always append `"--remote upstream"` to select the official remote, just like when locking manually.

First, notify the Discord server that you are (if you have the permissions) or would like to lock certain files to work on. After they are locked, make your edits and file a PR to a PCB uprev branch, or the `cad-staging` branch in the main repo (feature or bugfix branches with only code do not require locking; have a Contributor make a branch in the main repo for your edits if the branch does not already exist). Once your work has been merged into the main Aquarius repo, release the lock or have a Collaborator do it for you.

Even though you won't be locking files yourself, you still need Git LFS installed to view the files. Instead of storing the binary directly in the repo, Git LFS just stores a hash of the file in the repo, and puts the binary in a separate server. If you don't have LFS installed, some files might not be able to open properly. If you have it installed, Git LFS will take care of everything behind the scenes and your normal git commands will work as expected.

The only files that we lock using `git lfs` are `.FStd` files (for FreeCAD), plus `.sch` and `.kicad_pcb` files for KiCAD.

**It's important to note that if you don't have the files locked before you start working, we might not be able to merge your work. Make sure to get any KiCAD or FreeCAD files locked before starting work.** -->

## Branch Methodology
We are using Git for some things it's not designed to be used for, so we have a very considered branch methodology so that things can work well together. Please be sure to follow the guidelines below.

In general, we only ever merge to main from another branch in the CRGMakes repo. **Do not** file a pull request to the master branch.

<!-- ### CAD
Locking files with Git LFS solves the problem of impossible merge conflicts, but if no one is allowed to touch those files until they're merged, that greatly blocks progress. To address this, we maintain a `cad-staging` branch. This branch is where files can be checked in and out quickly and easily, and edits are pushed often. One person could lock a file, edit it, push it to the `cad-staging` branch, and unlock in a matter of minutes. Immediately, other folks can pull down those changes and make edits on the same file, not at all blocked by a PR that is still being validated. Once the `cad-staging` branch is ready for release all edited files are upreved, and it's merged into `master`, but not deleted. It is a perpetual branch upon which all CAD changes are made.

**All CAD changes must be made to the `cad-staging` branch.** If you're a contributor, commit directly to the branch. If you're not, have a Contributor lock the files for you, and file a PR from your fork to the `cad-staging` branch. Have the lock removed once your PR gets merged. If you're making a larger change that requires a code/PCB change along with the CAD, file a PR to the relevant feature branch with the PCB and code changes, and commit your CAD changes directly to `cad-staging`. -->

### PCBs
PCB progress is done in a branch dedicated to the next revision of the PCB (for example, a `v15` branch). This branch is in the crgmakes/aquarius repository. If you're a contributor, lock the files you're working on, commit directly to the feature branch, then unlock them. If you're not, have a Contributor lock the files for you, make your edits, and file a PR from your fork to the relevant feature branch. When the board is validated and ready for release, the branch is merged into `master` and the feature branch is closed. Relevant code to the PCB change can also be included in this feature branch, but **not CAD changes**.

### Code
Code is much, much easier to handle in git. Features or defects get their own branch in the crgmakes/aquariusp repo, and Contributors can commit directly to the branch; folks that are not contributors can file a PR to that branch.

### Docs
Docs are also easy to handle in git! They live in a [different repository](https://github.com/crgmakes/aquarius-docs).

## Making a Change
Now that you have forked the repo to your machine and have some files locked, it's time to get going! Make sure that your fork is up to date with the main repo (you can see how to do that [here](https://www.youtube.com/watch?v=deEYHVpE1c8&ab_channel=FaradayAcademy)). Checkout the relevant feature branch in your fork and go for it! Commit frequently with descriptive commit messages. Once you're finished, push up to your fork and file a Pull Request. Be sure to tag any relevant Issues that your PR is relevant to or solves.

### Versioning

#### Build Numbers
There are version numbers for releases, called **build numbers**. There's a release every time a feature or defect branch is merged into main, and there's a new tag on the `main` branch. Releases are tagged using a version number in the style of [semantic versioning](https://semver.org/), where, in part number `vA.B.C`:
- `A` uprevs indicate a large change in the project that could be backwards-compatibility breaking, or major releases with lots of significant updates.
- `B` uprevs indicate feature adds, large code reworks, CAD improvements, PCB revision releases, and other moderate changes. These are backwards compatible.
- `C` uprevs indicate small bug fixes, typos, or other small changes.

### Standards
The following are standards that we adopt across the project. They help make the project easier to build, reduce part count, and reduce cost.

**Mechanical**
* All parts are modeled separately and then put into a final assembly file.
* Stick to Metric unless absolutely necessary to do otherwise (eg. off the shelf part only has 1/4-20 threading available)
    * Use M3 and M5 hardware whenever possible. We use these across the build and keeping them standard reduces part count.
* Favor captive nuts as opposed to heat set inserts. They are easier to install, much cheaper, and much less likely to pull out.
* All custom parts should heavily consider printability in FDM. Try to allow parts to fit within a 150mm X 150mm X 150mm build volume. Design your parts around printing support-free.
* Ensure that any fonts used in your FreeCAD files use a **relative filepath.** Absolute filepaths will not work on other computers. Make sure you're only using fonts in the `/lib/fonts` folder in the repo.
* Every FDM part must have a ShapeString titled "PN" containing the part's Part Number, including revision (ex "FDM-0005-02"). This is so that the CI can automatically export the part with the correct name. First, go to the Dr

**Electrical**
* 4-layer boards are standard. Primarily because it's not that much more expensive and it provides greater power delivery and noise isolation.
* Choose an SMD part instead of a THT part. This makes it easier to fabricate the board using a pick and place.
* All passives should be 0603, unless it is absolutely necessary to deviate. This is to aid in reliability of being picked and placed, but also so that folks can easily hand solder if they wish.
* If possible, use components that are already in the BOM to reduce unique part count.
* Ensure that any components added to the BOM have at least two sources that ship globally with large stock (Digikey, Mouser, LCSC are good ones to check).
* Ensure that any footprint, symbol, etc files you use in a design are referenced using a **relative filepath.** Absolute filepaths will not work on other computers. Make sure you're only using files that are in the stock `kicad` folder or are provided in the `kicad-library` in the Aquarius git repo.

## Full Workflow
1. Hop in the [Discord](https://discord.gg/z89v73tU) and chat about the changes you'd like to make. Be sure to include the issue number that your change will address. (No issue yet? Make one, and mention it when discussing in Discord.)
2. Have one of the Collaborators lock the files you need to edit in your stead.
3. Ensure that [your fork is up to date with the main repo](https://www.youtube.com/watch?v=deEYHVpE1c8&ab_channel=FaradayAcademy).
4. Checkout the branch you'll be making edits to. If it's a CAD change, make them to `cad-staging`. If it's PCB changes, make them to the relevant branch for that PCB uprev. If you're making code changes, have a Contributor add a feature branch for you if it does not already exist.
5. Make changes. Commit often.
6. Push your changes to your fork on Github.
7. If a Contributor, push your changes to the relevant branch. If not file a Pull Request into the main repo's relevant feature branch.
8. Once your work is in the main repo (through Contributor direct commit, or PR if not a Contributor), unlock the files (or have a Contributor do it for you).
9. Close any issues that have been fixed by your changes.

# Working With Issues
All feature requests, defects, and planned enhancements are logged as Issues in Github. There are multiple different tags that we use to keep track of them. There are four types of tags:

**Product:**
These indicate which product the issue is relevant to. Choose `node`, `relay`, or `current`

**Type:**
These indicate if it's fixing an active problem, or an improvement. Either `defect` or `enhancement`

**Discipline:**
These indicate what skillset is required to complete the task. All relevant from the following should be chosen: `cad`, `code`, `pcb`, `automation`, or `documentation`

**Misc:**
These indicate an extra bit of info that can be helpful to filter by. `help wanted` and `good first issue` are helpful for folks looking to help contribute. `requires validation` and `discuss` indicate a bit of prototype, testing, or conversation needs to be done before work on the issue can begin. `wontfix` is for issues we've decided not to pursue. `duplicate` is for issues that already have an issue, and should be closed shortly after tagging as such.