# Static code analysis

(from ORFS-60)

## Background

We have code-climate, coveralls.io and houndci already operational on our code, and it would be nice to add coverity static analysis as well to identify any potential security issues that it might find.

## Goals

- enable coverity code scanning with TravisCI support (https://scan.coverity.com/travis_ci)
- determine potential value and potentially gate PR's on it's suggestions

## API
