# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.3.0] - 2026-08-18

### Changed

- mongo:5.0 -> 4.2
- OSパッケージ(Ubuntu 18.04/bionic)を最新化するため apt-get upgrade を追加。
  MongoDB社の4.2向けaptリポジトリは署名鍵が失効しているため、
  OS更新中のみ一時的に無効化してからapt-get update/upgradeを実行する。

## [0.2.0] - 2023-05-25

### Changed

- mongo:4.2 -> 5.0

## [0.1.0] - 2022-04-11

### Added

- Mirror mongo:4.2
