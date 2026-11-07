---
title: "When analyzing Dart exceptions, the exception rate is calculated using the session count. How is the session count defined? How are Dart exceptions counted?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Analyzing_Dart_exceptions_calc_exception_rate_by_session_count_How_define_session_count_and_count_"
---

Session count refers to the number of user session visits, with each session defined as the period from entering a page until turning off the page.

The denominator is the number of sessions in which Flutter was started. The method for calculating the session count is consistent with that used for native sessions. A session in which Flutter was started means that Flutter was running when the session was being calculated.
