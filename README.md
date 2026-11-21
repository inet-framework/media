# INET media

This repository holds the media of the INET documentation: the chart images, network images, screenshots and videos of the showcases and tutorials of [INET](https://github.com/inet-framework/inet). The `doc/media` folder of a showcase in INET is a link into this repository.

## Chart baselines

The chart images are also the stored results of the chart tests of INET. The test draws each chart of the analysis file (`.anf`) of a showcase, and compares the image with the image in this repository. A chart whose image file name is set in the analysis file is a result. The other files are documentation media.

## How INET uses this repository

Each INET commit pins one commit of this repository: the `ref` of the `chart` entry of `test_parameters` in `inet.opp`. The tests and the documentation of that INET commit use the files of that commit. The command `opp_checkout_test_baselines` of [opp_repl](https://github.com/omnetpp/opp_repl) clones this repository into the folder `media` of INET and checks out the pin.

`master` is the pin of INET `master`. After an INET change lands, `master` moves to its pin by a fast-forward.

## Change a chart

The procedure is in the INET guide [change-a-baseline.md](https://github.com/inet-framework/inet/blob/master/doc/project/guide/change-a-baseline.md), and the rules are `TR-BASELINE-*` in [testing.md](https://github.com/inet-framework/inet/blob/master/doc/project/rule/testing.md). In short:

- The INET commit that moves a chart changes the pin, in the same commit.
- One INET commit has at most one commit in this repository that changes chart images.
- The message of that commit holds the record: an analysis that says how each picture changes and why, the `Moved results:` block that `doc/project/enforcement/baseline_summary.py` of INET computes, and the trailers `INET-Subject:` and `Attribution:`. A reduction patch goes into the folder `attribution/`.
- Draw the images in the CI environment: the artifact of a CI run, or a copy of the CI job.

A commit that changes only documentation media needs no record. The pin can move over it.

## Review

Push a branch with the name of the INET branch, or open a pull request from a fork of this repository. The review of that branch or pull request approves the images. Name it in the description of the INET pull request.
