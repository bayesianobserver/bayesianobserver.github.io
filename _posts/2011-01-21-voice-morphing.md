---
layout: post
title: "Voice Morphing in Real time can break voice authentication"
date: 2011-01-21
mathjax: true
---

http://mi.eng.cam.ac.uk/~hy216/VoiceMorphingPrj.html Why this is so cool (and dangerous): Imagine that I have a large enough sample of your voice (if I have access to some of your phone messages, or voice chats, this is easy). I can then go and build a model of your voice. Using the technique in the papers above, I can then transform my voice into your voice *in real time*. This means that I maybe able to defeat a speaker-recognition/speaker-verification system, thereby breaking biometric systems that rely on voice for authentication. For example, if the biometric system asks me to speak a particular random phrase or sentence, I speak into a computer, that modifies my voice to sound like your voice in software, and then plays it back to the biometric system. Biometric systems should have 2 or 3 factor authentication -- biometric alone are broken!
