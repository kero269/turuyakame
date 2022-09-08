---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
url: "p/{{ template "permanentId" }}/"
archives: ["2022-09"] # !!!!!!
categories: [] # fill in [example, test]
tags: [] # fill in [example, test]
description: ""  # add description
summary: ""
draft: true
---

{{ define "permanentId" -}}
{{- $scratch := newScratch -}}
{{- range (seq 7) -}}
{{- $nextCh := slice "2" "3" "4" "5" "6" "7" "8" "9" "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "m" "n" "o" "p" "q" "r" "s" "t" "u" "v" "w" "x" "y" "z" | shuffle | first 1 -}}
{{- $scratch.Add "id" $nextCh -}}
{{- end -}}
{{- delimit ($scratch.Get "id") "" -}}
{{- end -}}
