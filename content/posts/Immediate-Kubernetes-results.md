---
layout: post
date: 2021-08-10T11:54:27-05:00
title: Immediate Kubernetes Certification Exam results 
tags: ["Kubernetes", "CKA", "CKAD", "k8s"]
---

<img src="/img/CKACert.jpg" alt="CKA Certificate" style="width:350px;display:inline">
<img src="/img/CKADCert.jpg" alt="CKAD Certificate" style="width:350px;display:inline">

I recently passed CKA and CKAD (yay me!).

Being that I'm very impatient and I couldn't wait the 24 hours for my result. For people who haven't attempted the Certified Kubernetes exams, there's a [24 hour period](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks#how-is-my-exam-scored) between completing your exam and receiving the results.

So after I attempted CKAD (which came after CKA for me), I started inspecting the API calls. Users on Reddit pointed out that that exams are automatically marked and I wondered if there's a way to figure out scores before 24 hour period.

I started combing through API calls made on the LinuxFoundation Training Portal exam page using my browser's developer tool Network tab. After spending some time on it, I couldn't believe that score was right there being returned by the backend. I reckon, there's a timer in frontend JavaScript to not display scores until the timer hits 0.

It was a `GET` call to endpoint below. 

`https://lfx-bff.platform.linuxfoundation.org/api/faraday/reservations/active?exam=CKAD&email=mypersonal@email.com&name=Ahmed%2520Sajid&ldap_username=username`

<img src="/img/CKADScoreAPICall.jpg" alt="CKAD Score API Call">
