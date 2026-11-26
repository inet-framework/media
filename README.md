# INET media

This repository holds the media of the INET documentation: the chart images, network images, screenshots and videos of the showcases and tutorials of [INET](https://github.com/inet-framework/inet). The `doc/media` folder of a showcase in INET is a link into this repository.

## Chart baselines

The chart images are also the stored results of the chart tests of INET. The test draws each chart of the analysis file (`.anf`) of a showcase, and compares the image with the image in this repository. A chart whose image file name is set in the analysis file is a result. The other files are documentation media.

## How INET uses this repository

Each INET commit has one commit of this repository as its baseline. The tests and the documentation of that INET commit use the files of that commit. The command `opp_checkout_test_baselines` of [opp_repl](https://github.com/omnetpp/opp_repl) clones this repository into the folder `media` of INET and checks out the baseline of the INET commit.

An INET commit that moves a chart has the trailer `Chart-Baseline: <hash>` in its message: the pin, the last commit of its step on a branch of this repository. `inet.opp` does not change. After the INET change lands, the landing job of INET (`check-baseline-masters.yml`) puts the steps onto `master`: by a fast-forward when a step starts on the head of `master`, and else by a rebase, with the same messages and authors. After the steps it adds a mark: a commit with no change of files, with the line `Baseline-Of: <INET hash> <baseline hash>` for each landed INET commit. Thus `master` holds the baseline of INET `master`.

A file that a branch changes and that `master` changed since the base of the branch is an overlap, and the landing stops. The commit status `Baseline merge` of the INET pull request shows an overlap before the landing.

After a rebase, the head of a pull request of this repository is not on `master`, so GitHub does not mark it as merged. The mark names it in the line `Baseline-Pull-Request: #N`, the log and the job summary of the landing job name it too, and a maintainer closes it.

## Change a chart

The procedure is in the INET guide [change-a-baseline.md](https://github.com/inet-framework/inet/blob/master/doc/project/guide/change-a-baseline.md), and the rules are `TR-BASELINE-*` in [testing.md](https://github.com/inet-framework/inet/blob/master/doc/project/rule/testing.md). In short:

- The INET commit that moves a chart has the pin trailer.
- One INET commit has at most one commit in this repository that changes chart images.
- The message of that commit holds the record: an analysis that says how each picture changes and why, the `Moved results:` block that `doc/project/enforcement/baseline_summary.py` of INET computes, and the trailers `INET-Subject:` and `Attribution:`. A reduction patch goes into the folder `attribution/`.
- Draw the images in the CI environment: the artifact of a CI run, or a copy of the CI job.

A commit that changes only documentation media needs no record. A step can go over it.

## Review

Start the branch on the head of `master`. Push a branch with the name of the INET branch, or open a pull request from a fork of this repository. Do not merge the pull request with the button: the landing job lands it. The review of that branch or pull request approves the images. Name it in the description of the INET pull request.
