---
title: "SMS pricing"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-pricing"
---

<span id="bc3cb63f"></span>
## Billing calculation

For each billing cycle, the total charge is calculated using the formula below:

**Total Charge = Unit Price × Number of SMS Segments**


* **Unit Price**: The per\-segment price for the destination country or area, as listed in the pricing table below.

* **Number of SMS Segments**: The total number of SMS segments passed to downstream providers within the billing cycle. A long message that exceeds the character limit is split into multiple segments (see [Character limit](https://docs.byteplus.com/en/docs/20/7173#character-limit)), and each segment is billed individually.


The final billable amount for each billing cycle is **rounded using standard rounding rules**.

<span id="character-limit"></span>
## Character limit

BytePlus SMS uses GSM\-7 character set to determine SMS character limit. For messages encoded using the GSM\-7 character set, the character limit is 160 characters; For messages not encoded with GSM\-7, it is 70 characters. A large message containing over 160 characters or 70 characters will be split into individual SMS messages, also known as segments, and recreated at the receiving end.


* **Messages encoded using the GSM\-7 character set**: One text message can contain up to 160 characters, including spaces. For messages exceeding 160 characters, the content will be broken down into chunks, with each chunk containing a maximum of 153 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you send an English text message containing 500 characters, including spaces, then your message will be broken into chunks of 153 characters. So, in total, you will send three messages of 153 characters and one message of 41 characters.</div>



* **Messages not encoded with GSM\-7 character set**: One text message can contain a maximum of 70 characters, including spaces. For messages exceeding 70 characters, the content will be broken down into chunks, with each chunk containing a maximum of 67 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you send a text message that includes languages other than English and it contains 200 characters, including spaces, then your message will be broken down into chunks of 67 characters. So, in total, you will send two messages of 67 characters and one message of 66 characters.</div>


<span id="6f5dc8c3"></span>
## Pricing

The table below contains the up\-to\-date pricing for countries or areas.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Service fees are charged when the messages are passed to SMS carriers or CPaaS Providers, regardless of whether the messages are successfully sent to Recipients or not.</div>



|<div style="text-align: center"><br>Market</div><br> |<div style="text-align: center"><br>ISO Code</div><br> |Unit Price (USD） ||
|---|---|---|---|
|||BytePlus Multi\-routing |BytePlus SMS |
|<div style="text-align: center"><br>Ascension i.</div><br> |<div style="text-align: center"><br>AC</div><br> |0.0623 |0.1207 |
|<div style="text-align: center"><br>Andorra</div><br> |<div style="text-align: center"><br>AD</div><br> |0.0899 |0.0948 |
|<div style="text-align: center"><br>United Arab Emirates</div><br> |<div style="text-align: center"><br>AE</div><br> |0.0344 |0.1012 |
|<div style="text-align: center"><br>Afghanistan</div><br> |<div style="text-align: center"><br>AF</div><br> |0.2337 |0.3507 |
|<div style="text-align: center"><br>Antigua and Barbuda</div><br> |<div style="text-align: center"><br>AG</div><br> |0.0778 |0.1129 |
|<div style="text-align: center"><br>Anguilla</div><br> |<div style="text-align: center"><br>AI</div><br> |0.1096 |0.0868 |
|<div style="text-align: center"><br>Albania</div><br> |<div style="text-align: center"><br>AL</div><br> |0.037 |0.0824 |
|<div style="text-align: center"><br>Armenia</div><br> |<div style="text-align: center"><br>AM</div><br> |0.0969 |0.2059 |
|<div style="text-align: center"><br>Angola</div><br> |<div style="text-align: center"><br>AO</div><br> |0.0248 |0.0777 |
|<div style="text-align: center"><br>Argentina</div><br> |<div style="text-align: center"><br>AR</div><br> |0.0507 |0.0993 |
|<div style="text-align: center"><br>American Samoa</div><br> |<div style="text-align: center"><br>AS</div><br> |0.0567 |0.0596 |
|<div style="text-align: center"><br>Austria</div><br> |<div style="text-align: center"><br>AT</div><br> |0.029 |0.029 |
|<div style="text-align: center"><br>Australia</div><br> |<div style="text-align: center"><br>AU</div><br> |0.0159 |0.0159 |
|<div style="text-align: center"><br>Aruba</div><br> |<div style="text-align: center"><br>AW</div><br> |0.0951 |0.1304 |
|<div style="text-align: center"><br>Åland Islands</div><br> |<div style="text-align: center"><br>AX</div><br> |0.1059 |0.1511 |
|<div style="text-align: center"><br>Azerbaijan</div><br> |<div style="text-align: center"><br>AZ</div><br> |0.2285 |0.2285 |
|<div style="text-align: center"><br>Bosnia and Herzegovina</div><br> |<div style="text-align: center"><br>BA</div><br> |0.054 |0.1004 |
|<div style="text-align: center"><br>Barbados</div><br> |<div style="text-align: center"><br>BB</div><br> |0.0831 |0.1551 |
|<div style="text-align: center"><br>Bangladesh</div><br> |<div style="text-align: center"><br>BD</div><br> |0.0104 |0.325 |
|<div style="text-align: center"><br>Belgium</div><br> |<div style="text-align: center"><br>BE</div><br> |0.059 |0.0634 |
|<div style="text-align: center"><br>Burkina Faso</div><br> |<div style="text-align: center"><br>BF</div><br> |0.0789 |0.1667 |
|<div style="text-align: center"><br>Bulgaria</div><br> |<div style="text-align: center"><br>BG</div><br> |0.1338 |0.1232 |
|<div style="text-align: center"><br>Bahrain</div><br> |<div style="text-align: center"><br>BH</div><br> |0.0208 |0.0284 |
|<div style="text-align: center"><br>Burundi</div><br> |<div style="text-align: center"><br>BI</div><br> |0.0687 |0.3464 |
|<div style="text-align: center"><br>Benin</div><br> |<div style="text-align: center"><br>BJ</div><br> |0.0814 |0.2591 |
|<div style="text-align: center"><br>Bermuda</div><br> |<div style="text-align: center"><br>BM</div><br> |0.092 |0.1722 |
|<div style="text-align: center"><br>Brunei</div><br> |<div style="text-align: center"><br>BN</div><br> |0.0064 |0.0329 |
|<div style="text-align: center"><br>Bolivia</div><br> |<div style="text-align: center"><br>BO</div><br> |0.0644 |0.132 |
|<div style="text-align: center"><br>Dutch Caribbean</div><br> |<div style="text-align: center"><br>BQ</div><br> |0.1064 |0.1164 |
|<div style="text-align: center"><br>Brazil</div><br> |<div style="text-align: center"><br>BR</div><br> |0.0121 |0.0133 |
|<div style="text-align: center"><br>Bahamas</div><br> |<div style="text-align: center"><br>BS</div><br> |0.039 |0.0945 |
|<div style="text-align: center"><br>Bhutan</div><br> |<div style="text-align: center"><br>BT</div><br> |0.1741 |0.2496 |
|<div style="text-align: center"><br>Botswana</div><br> |<div style="text-align: center"><br>BW</div><br> |0.0268 |0.0656 |
|<div style="text-align: center"><br>Belarus</div><br> |<div style="text-align: center"><br>BY</div><br> |0.1617 |0.1805 |
|<div style="text-align: center"><br>Belize</div><br> |<div style="text-align: center"><br>BZ</div><br> |0.1402 |0.2782 |
|<div style="text-align: center"><br>Canada</div><br> |<div style="text-align: center"><br>CA</div><br> |0.0159 |0.0235 |
|<div style="text-align: center"><br>DR Congo</div><br> |<div style="text-align: center"><br>CD</div><br> |0.063 |0.1878 |
|<div style="text-align: center"><br>Central African Republic</div><br> |<div style="text-align: center"><br>CF</div><br> |0.0208 |0.1163 |
|<div style="text-align: center"><br>Republic of Congo</div><br> |<div style="text-align: center"><br>CG</div><br> |0.0631 |0.1858 |
|<div style="text-align: center"><br>Switzerland</div><br> |<div style="text-align: center"><br>CH</div><br> |0.04 |0.04 |
|<div style="text-align: center"><br>Ivory Coast</div><br> |<div style="text-align: center"><br>CI</div><br> |0.055 |0.2662 |
|<div style="text-align: center"><br>Cook Islands</div><br> |<div style="text-align: center"><br>CK</div><br> |0.1296 |0.1249 |
|<div style="text-align: center"><br>Chile</div><br> |<div style="text-align: center"><br>CL</div><br> |0.0085 |0.0085 |
|<div style="text-align: center"><br>Cameroon</div><br> |<div style="text-align: center"><br>CM</div><br> |0.0649 |0.2516 |
|<div style="text-align: center"><br>China Mainland</div><br> |<div style="text-align: center"><br>CN</div><br> |0.0116 |0.0116 |
|<div style="text-align: center"><br>Colombia</div><br> |<div style="text-align: center"><br>CO</div><br> |0.0007 |0.001 |
|<div style="text-align: center"><br>Costa rica</div><br> |<div style="text-align: center"><br>CR</div><br> |0.022 |0.012 |
|<div style="text-align: center"><br>Cape verde</div><br> |<div style="text-align: center"><br>CV</div><br> |0.0854 |0.1454 |
|<div style="text-align: center"><br>Curacao</div><br> |<div style="text-align: center"><br>CW</div><br> |0.103 |0.2601 |
|<div style="text-align: center"><br>Cyprus</div><br> |<div style="text-align: center"><br>CY</div><br> |0.0133 |0.0118 |
|<div style="text-align: center"><br>Czech Republic</div><br> |<div style="text-align: center"><br>CZ</div><br> |0.0568 |0.0518 |
|<div style="text-align: center"><br>Germany</div><br> |<div style="text-align: center"><br>DE</div><br> |0.0621 |0.1038 |
|<div style="text-align: center"><br>Djibouti</div><br> |<div style="text-align: center"><br>DJ</div><br> |0.0779 |0.1445 |
|<div style="text-align: center"><br>Denmark</div><br> |<div style="text-align: center"><br>DK</div><br> |0.0464 |0.0464 |
|<div style="text-align: center"><br>Dominica</div><br> |<div style="text-align: center"><br>DM</div><br> |0.1311 |0.1201 |
|<div style="text-align: center"><br>Dominican Republic</div><br> |<div style="text-align: center"><br>DO</div><br> |0.0409 |0.0552 |
|<div style="text-align: center"><br>Algeria</div><br> |<div style="text-align: center"><br>DZ</div><br> |0.1309 |0.249 |
|<div style="text-align: center"><br>Ecuador</div><br> |<div style="text-align: center"><br>EC</div><br> |0.0621 |0.1665 |
|<div style="text-align: center"><br>Estonia</div><br> |<div style="text-align: center"><br>EE</div><br> |0.0324 |0.0347 |
|<div style="text-align: center"><br>Egypt</div><br> |<div style="text-align: center"><br>EG</div><br> |0.0347 |0.2917 |
|<div style="text-align: center"><br>Western Sahara</div><br> |<div style="text-align: center"><br>EH</div><br> |0.1039 |0.0959 |
|<div style="text-align: center"><br>Eritrea</div><br> |<div style="text-align: center"><br>ER</div><br> |0.0935 |0.0906 |
|<div style="text-align: center"><br>Spain</div><br> |<div style="text-align: center"><br>ES</div><br> |0.0187 |0.0381 |
|<div style="text-align: center"><br>Ethiopia</div><br> |<div style="text-align: center"><br>ET</div><br> |0.1264 |0.2862 |
|<div style="text-align: center"><br>Finland</div><br> |<div style="text-align: center"><br>FI</div><br> |0.0631 |0.0631 |
|<div style="text-align: center"><br>Fiji</div><br> |<div style="text-align: center"><br>FJ</div><br> |0.097 |0.1675 |
|<div style="text-align: center"><br>Falkland Islands</div><br> |<div style="text-align: center"><br>FK</div><br> |0.0374 |0.0672 |
|<div style="text-align: center"><br>The Federated States of Micronesia</div><br> |<div style="text-align: center"><br>FM</div><br> |0.0415 |0.0784 |
|<div style="text-align: center"><br>Faroe Islands</div><br> |<div style="text-align: center"><br>FO</div><br> |0.0395 |0.0764 |
|<div style="text-align: center"><br>France</div><br> |<div style="text-align: center"><br>FR</div><br> |0.045 |0.0541 |
|<div style="text-align: center"><br>Gabon</div><br> |<div style="text-align: center"><br>GA</div><br> |0.112 |0.2011 |
|<div style="text-align: center"><br>United Kingdom</div><br> |<div style="text-align: center"><br>GB</div><br> |0.0355 |0.0399 |
|<div style="text-align: center"><br>Grenada</div><br> |<div style="text-align: center"><br>GD</div><br> |0.1039 |0.147 |
|<div style="text-align: center"><br>Georgia</div><br> |<div style="text-align: center"><br>GE</div><br> |0.1257 |0.1177 |
|<div style="text-align: center"><br>French Guiana</div><br> |<div style="text-align: center"><br>GF</div><br> |0.1003 |0.0844 |
|<div style="text-align: center"><br>Guernsey</div><br> |<div style="text-align: center"><br>GG</div><br> |0.0486 |0.0918 |
|<div style="text-align: center"><br>Ghana</div><br> |<div style="text-align: center"><br>GH</div><br> |0.0645 |0.278 |
|<div style="text-align: center"><br>Gibraltar</div><br> |<div style="text-align: center"><br>GI</div><br> |0.0374 |0.1284 |
|<div style="text-align: center"><br>Greenland</div><br> |<div style="text-align: center"><br>GL</div><br> |0.0235 |0.0202 |
|<div style="text-align: center"><br>Gambia</div><br> |<div style="text-align: center"><br>GM</div><br> |0.0895 |0.2655 |
|<div style="text-align: center"><br>Guinea</div><br> |<div style="text-align: center"><br>GN</div><br> |0.0828 |0.2945 |
|<div style="text-align: center"><br>Guadeloupe</div><br> |<div style="text-align: center"><br>GP</div><br> |0.0881 |0.1863 |
|<div style="text-align: center"><br>Equatorial Guinea</div><br> |<div style="text-align: center"><br>GQ</div><br> |0.0742 |0.221 |
|<div style="text-align: center"><br>Greece</div><br> |<div style="text-align: center"><br>GR</div><br> |0.0341 |0.0495 |
|<div style="text-align: center"><br>Guatemala</div><br> |<div style="text-align: center"><br>GT</div><br> |0.0623 |0.2124 |
|<div style="text-align: center"><br>Guam</div><br> |<div style="text-align: center"><br>GU</div><br> |0.0136 |0.0841 |
|<div style="text-align: center"><br>Guinea\-Bissau</div><br> |<div style="text-align: center"><br>GW</div><br> |0.05 |0.2864 |
|<div style="text-align: center"><br>Guyana</div><br> |<div style="text-align: center"><br>GY</div><br> |0.0866 |0.1711 |
|<div style="text-align: center"><br>Hong Kong</div><br> |<div style="text-align: center"><br>HK</div><br> |0.0413 |0.0557 |
|<div style="text-align: center"><br>Honduras</div><br> |<div style="text-align: center"><br>HN</div><br> |0.0574 |0.1157 |
|<div style="text-align: center"><br>Croatia</div><br> |<div style="text-align: center"><br>HR</div><br> |0.0486 |0.1071 |
|<div style="text-align: center"><br>Haiti</div><br> |<div style="text-align: center"><br>HT</div><br> |0.0861 |0.147 |
|<div style="text-align: center"><br>Hungary</div><br> |<div style="text-align: center"><br>HU</div><br> |0.0583 |0.0583 |
|<div style="text-align: center"><br>Indonesia</div><br> |<div style="text-align: center"><br>ID</div><br> |0.0898 |0.3562 |
|<div style="text-align: center"><br>Ireland</div><br> |<div style="text-align: center"><br>IE</div><br> |0.065 |0.065 |
|<div style="text-align: center"><br>Israel</div><br> |<div style="text-align: center"><br>IL</div><br> |0.0519 |0.2216 |
|<div style="text-align: center"><br>Isle of Man</div><br> |<div style="text-align: center"><br>IM</div><br> |0.0889 |0.0521 |
|<div style="text-align: center"><br>India</div><br> |<div style="text-align: center"><br>IN</div><br> |0.0156 |0.0637 |
|<div style="text-align: center"><br>British Indian Ocean Territory</div><br> |<div style="text-align: center"><br>IO</div><br> |0.0592 |0.0794 |
|<div style="text-align: center"><br>Iraq</div><br> |<div style="text-align: center"><br>IQ</div><br> |0.1101 |0.3458 |
|<div style="text-align: center"><br>Iceland</div><br> |<div style="text-align: center"><br>IS</div><br> |0.0713 |0.0718 |
|<div style="text-align: center"><br>Italy</div><br> |<div style="text-align: center"><br>IT</div><br> |0.0349 |0.0465 |
|<div style="text-align: center"><br>Jersey</div><br> |<div style="text-align: center"><br>JE</div><br> |0.0631 |0.078 |
|<div style="text-align: center"><br>Jamaica</div><br> |<div style="text-align: center"><br>JM</div><br> |0.0727 |0.171 |
|<div style="text-align: center"><br>Jordan</div><br> |<div style="text-align: center"><br>JO</div><br> |0.0831 |0.3672 |
|<div style="text-align: center"><br>Japan</div><br> |<div style="text-align: center"><br>JP</div><br> |0.0315 |0.046 |
|<div style="text-align: center"><br>Kenya</div><br> |<div style="text-align: center"><br>KE</div><br> |0.0332 |0.0998 |
|<div style="text-align: center"><br>Kyrgyzstan</div><br> |<div style="text-align: center"><br>KG</div><br> |0.1464 |0.3351 |
|<div style="text-align: center"><br>Cambodia</div><br> |<div style="text-align: center"><br>KH</div><br> |0.0786 |0.3151 |
|<div style="text-align: center"><br>Kiribati</div><br> |<div style="text-align: center"><br>KI</div><br> |0.0967 |0.0527 |
|<div style="text-align: center"><br>Comoros</div><br> |<div style="text-align: center"><br>KM</div><br> |0.0919 |0.1159 |
|<div style="text-align: center"><br>Saint Kitts and Nevis</div><br> |<div style="text-align: center"><br>KN</div><br> |0.1039 |0.1492 |
|<div style="text-align: center"><br>South Korea</div><br> |<div style="text-align: center"><br>KR</div><br> |0.0128 |0.0128 |
|<div style="text-align: center"><br>Kuwait</div><br> |<div style="text-align: center"><br>KW</div><br> |0.1207 |0.276 |
|<div style="text-align: center"><br>Cayman Islands</div><br> |<div style="text-align: center"><br>KY</div><br> |0.1039 |0.1379 |
|<div style="text-align: center"><br>Kazakhstan</div><br> |<div style="text-align: center"><br>KZ</div><br> |0.038 |0.2778 |
|<div style="text-align: center"><br>Laos</div><br> |<div style="text-align: center"><br>LA</div><br> |0.0357 |0.1381 |
|<div style="text-align: center"><br>Lebanon</div><br> |<div style="text-align: center"><br>LB</div><br> |0.0831 |0.2736 |
|<div style="text-align: center"><br>St. Lucia</div><br> |<div style="text-align: center"><br>LC</div><br> |0.0912 |0.132 |
|<div style="text-align: center"><br>Liechtenstein</div><br> |<div style="text-align: center"><br>LI</div><br> |0.044 |0.0215 |
|<div style="text-align: center"><br>Sri Lanka</div><br> |<div style="text-align: center"><br>LK</div><br> |0.0944 |0.3235 |
|<div style="text-align: center"><br>Liberia</div><br> |<div style="text-align: center"><br>LR</div><br> |0.0835 |0.1646 |
|<div style="text-align: center"><br>Lesotho</div><br> |<div style="text-align: center"><br>LS</div><br> |0.0539 |0.1406 |
|<div style="text-align: center"><br>Lithuania</div><br> |<div style="text-align: center"><br>LT</div><br> |0.0457 |0.047 |
|<div style="text-align: center"><br>Luxembourg</div><br> |<div style="text-align: center"><br>LU</div><br> |0.0744 |0.0744 |
|<div style="text-align: center"><br>Latvia</div><br> |<div style="text-align: center"><br>LV</div><br> |0.0368 |0.0426 |
|<div style="text-align: center"><br>Libya</div><br> |<div style="text-align: center"><br>LY</div><br> |0.1383 |0.3141 |
|<div style="text-align: center"><br>Morocco</div><br> |<div style="text-align: center"><br>MA</div><br> |0.0862 |0.2014 |
|<div style="text-align: center"><br>Monaco</div><br> |<div style="text-align: center"><br>MC</div><br> |0.0861 |0.1431 |
|<div style="text-align: center"><br>Moldova</div><br> |<div style="text-align: center"><br>MD</div><br> |0.0709 |0.0674 |
|<div style="text-align: center"><br>Montenegro</div><br> |<div style="text-align: center"><br>ME</div><br> |0.0568 |0.0741 |
|<div style="text-align: center"><br>Madagascar</div><br> |<div style="text-align: center"><br>MG</div><br> |0.1305 |0.3863 |
|<div style="text-align: center"><br>Marshall Islands</div><br> |<div style="text-align: center"><br>MH</div><br> |0.1122 |0.1504 |
|<div style="text-align: center"><br>Macedonia</div><br> |<div style="text-align: center"><br>MK</div><br> |0.0186 |0.0248 |
|<div style="text-align: center"><br>Mali</div><br> |<div style="text-align: center"><br>ML</div><br> |0.0887 |0.1766 |
|<div style="text-align: center"><br>Myanmar</div><br> |<div style="text-align: center"><br>MM</div><br> |0.0587 |0.2528 |
|<div style="text-align: center"><br>Mongolia</div><br> |<div style="text-align: center"><br>MN</div><br> |0.1377 |0.2654 |
|<div style="text-align: center"><br>Macao</div><br> |<div style="text-align: center"><br>MO</div><br> |0.0239 |0.0239 |
|<div style="text-align: center"><br>Northern Mariana Islands</div><br> |<div style="text-align: center"><br>MP</div><br> |0.0879 |0.1246 |
|<div style="text-align: center"><br>Martinique</div><br> |<div style="text-align: center"><br>MQ</div><br> |0.1009 |0.1185 |
|<div style="text-align: center"><br>Mauritania</div><br> |<div style="text-align: center"><br>MR</div><br> |0.0891 |0.1337 |
|<div style="text-align: center"><br>Montserrat</div><br> |<div style="text-align: center"><br>MS</div><br> |0.058 |0.0967 |
|<div style="text-align: center"><br>Malta</div><br> |<div style="text-align: center"><br>MT</div><br> |0.0505 |0.0573 |
|<div style="text-align: center"><br>Mauritius</div><br> |<div style="text-align: center"><br>MU</div><br> |0.0816 |0.1432 |
|<div style="text-align: center"><br>Maldives</div><br> |<div style="text-align: center"><br>MV</div><br> |0.0208 |0.1764 |
|<div style="text-align: center"><br>Malawi</div><br> |<div style="text-align: center"><br>MW</div><br> |0.103 |0.2363 |
|<div style="text-align: center"><br>Mexico</div><br> |<div style="text-align: center"><br>MX</div><br> |0.0054 |0.0054 |
|<div style="text-align: center"><br>Malaysia</div><br> |<div style="text-align: center"><br>MY</div><br> |0.0272 |0.2542 |
|<div style="text-align: center"><br>Mozambique</div><br> |<div style="text-align: center"><br>MZ</div><br> |0.0351 |0.0857 |
|<div style="text-align: center"><br>Namibia</div><br> |<div style="text-align: center"><br>NA</div><br> |0.0216 |0.0152 |
|<div style="text-align: center"><br>New Caledonia</div><br> |<div style="text-align: center"><br>NC</div><br> |0.0682 |0.1009 |
|<div style="text-align: center"><br>Niger</div><br> |<div style="text-align: center"><br>NE</div><br> |0.1089 |0.2066 |
|<div style="text-align: center"><br>Norfolk Island</div><br> |<div style="text-align: center"><br>NF</div><br> |0.0943 |0.0481 |
|<div style="text-align: center"><br>Nigeria</div><br> |<div style="text-align: center"><br>NG</div><br> |0.0291 |0.1853 |
|<div style="text-align: center"><br>Nicaragua</div><br> |<div style="text-align: center"><br>NI</div><br> |0.0474 |0.0904 |
|<div style="text-align: center"><br>Netherlands</div><br> |<div style="text-align: center"><br>NL</div><br> |0.0713 |0.0878 |
|<div style="text-align: center"><br>Norway</div><br> |<div style="text-align: center"><br>NO</div><br> |0.0609 |0.0539 |
|<div style="text-align: center"><br>Nepal</div><br> |<div style="text-align: center"><br>NP</div><br> |0.0956 |0.2863 |
|<div style="text-align: center"><br>Nauru</div><br> |<div style="text-align: center"><br>NR</div><br> |0.1018 |0.1511 |
|<div style="text-align: center"><br>Niue</div><br> |<div style="text-align: center"><br>NU</div><br> |0.1288 |0.0483 |
|<div style="text-align: center"><br>New Zealand</div><br> |<div style="text-align: center"><br>NZ</div><br> |0.0684 |0.0684 |
|<div style="text-align: center"><br>Oman</div><br> |<div style="text-align: center"><br>OM</div><br> |0.0706 |0.0979 |
|<div style="text-align: center"><br>Panama</div><br> |<div style="text-align: center"><br>PA</div><br> |0.087 |0.1155 |
|<div style="text-align: center"><br>Peru</div><br> |<div style="text-align: center"><br>PE</div><br> |0.0098 |0.0968 |
|<div style="text-align: center"><br>French Polynesia</div><br> |<div style="text-align: center"><br>PF</div><br> |0.0868 |0.0879 |
|<div style="text-align: center"><br>Papua New Guinea</div><br> |<div style="text-align: center"><br>PG</div><br> |0.1183 |0.1932 |
|<div style="text-align: center"><br>Philippines</div><br> |<div style="text-align: center"><br>PH</div><br> |0.0257 |0.1884 |
|<div style="text-align: center"><br>Pakistan</div><br> |<div style="text-align: center"><br>PK</div><br> |0.0412 |0.38 |
|<div style="text-align: center"><br>Poland</div><br> |<div style="text-align: center"><br>PL</div><br> |0.0207 |0.0207 |
|<div style="text-align: center"><br>Saint\-Pierre and Miquelon</div><br> |<div style="text-align: center"><br>PM</div><br> |0.1342 |0.1331 |
|<div style="text-align: center"><br>Puerto Rico</div><br> |<div style="text-align: center"><br>PR</div><br> |0.0148 |0.0097 |
|<div style="text-align: center"><br>Palestine</div><br> |<div style="text-align: center"><br>PS</div><br> |0.3402 |0.3631 |
|<div style="text-align: center"><br>Portugal</div><br> |<div style="text-align: center"><br>PT</div><br> |0.0179 |0.0179 |
|<div style="text-align: center"><br>Palau</div><br> |<div style="text-align: center"><br>PW</div><br> |0.027 |0.0463 |
|<div style="text-align: center"><br>Paraguay</div><br> |<div style="text-align: center"><br>PY</div><br> |0.0234 |0.1191 |
|<div style="text-align: center"><br>Qatar</div><br> |<div style="text-align: center"><br>QA</div><br> |0.0279 |0.1653 |
|<div style="text-align: center"><br>Reunion</div><br> |<div style="text-align: center"><br>RE</div><br> |0.0704 |0.072 |
|<div style="text-align: center"><br>Romania</div><br> |<div style="text-align: center"><br>RO</div><br> |0.0475 |0.0464 |
|<div style="text-align: center"><br>Serbia</div><br> |<div style="text-align: center"><br>RS</div><br> |0.0623 |0.3052 |
|<div style="text-align: center"><br>Russia</div><br> |<div style="text-align: center"><br>RU</div><br> |0.0466 |0.3516 |
|<div style="text-align: center"><br>Rwanda</div><br> |<div style="text-align: center"><br>RW</div><br> |0.0861 |0.2889 |
|<div style="text-align: center"><br>Saudi Arabia</div><br> |<div style="text-align: center"><br>SA</div><br> |0.0296 |0.1284 |
|<div style="text-align: center"><br>Solomon Islands</div><br> |<div style="text-align: center"><br>SB</div><br> |0.0465 |0.0671 |
|<div style="text-align: center"><br>Seychelles</div><br> |<div style="text-align: center"><br>SC</div><br> |0.0394 |0.0762 |
|<div style="text-align: center"><br>Sudan</div><br> |<div style="text-align: center"><br>SD</div><br> |0.0968 |0.3281 |
|<div style="text-align: center"><br>Sweden</div><br> |<div style="text-align: center"><br>SE</div><br> |0.0509 |0.0509 |
|<div style="text-align: center"><br>Singapore</div><br> |<div style="text-align: center"><br>SG</div><br> |0.0256 |0.0409 |
|<div style="text-align: center"><br>Saint Helena</div><br> |<div style="text-align: center"><br>SH</div><br> |0.1186 |0.1243 |
|<div style="text-align: center"><br>Slovenia</div><br> |<div style="text-align: center"><br>SI</div><br> |0.1729 |0.1378 |
|<div style="text-align: center"><br>Svalbard and Jan Mayen</div><br> |<div style="text-align: center"><br>SJ</div><br> |0.1288 |0.1554 |
|<div style="text-align: center"><br>Slovakia</div><br> |<div style="text-align: center"><br>SK</div><br> |0.0543 |0.0543 |
|<div style="text-align: center"><br>Sierra Leone</div><br> |<div style="text-align: center"><br>SL</div><br> |0.057 |0.2513 |
|<div style="text-align: center"><br>San Marino</div><br> |<div style="text-align: center"><br>SM</div><br> |0.0824 |0.0752 |
|<div style="text-align: center"><br>Senegal</div><br> |<div style="text-align: center"><br>SN</div><br> |0.0945 |0.1987 |
|<div style="text-align: center"><br>Somalia</div><br> |<div style="text-align: center"><br>SO</div><br> |0.104 |0.1858 |
|<div style="text-align: center"><br>Suriname</div><br> |<div style="text-align: center"><br>SR</div><br> |0.076 |0.0884 |
|<div style="text-align: center"><br>South Sudan</div><br> |<div style="text-align: center"><br>SS</div><br> |0.0915 |0.1501 |
|<div style="text-align: center"><br>Sao Tome and Principe</div><br> |<div style="text-align: center"><br>ST</div><br> |0.026 |0.0213 |
|<div style="text-align: center"><br>El Salvador</div><br> |<div style="text-align: center"><br>SV</div><br> |0.0436 |0.0448 |
|<div style="text-align: center"><br>Saint Martin</div><br> |<div style="text-align: center"><br>SX</div><br> |0.0802 |0.1221 |
|<div style="text-align: center"><br>Swaziland</div><br> |<div style="text-align: center"><br>SZ</div><br> |0.0555 |0.0822 |
|<div style="text-align: center"><br>Turks and Caicos Islands</div><br> |<div style="text-align: center"><br>TC</div><br> |0.081 |0.1064 |
|<div style="text-align: center"><br>Chad</div><br> |<div style="text-align: center"><br>TD</div><br> |0.1134 |0.2551 |
|<div style="text-align: center"><br>Togo</div><br> |<div style="text-align: center"><br>TG</div><br> |0.0717 |0.3584 |
|<div style="text-align: center"><br>Thailand</div><br> |<div style="text-align: center"><br>TH</div><br> |0.0058 |0.0058 |
|<div style="text-align: center"><br>Tajikistan</div><br> |<div style="text-align: center"><br>TJ</div><br> |0.2748 |0.3833 |
|<div style="text-align: center"><br>Tokelau</div><br> |<div style="text-align: center"><br>TK</div><br> |0.1246 |0.42 |
|<div style="text-align: center"><br>East Timor</div><br> |<div style="text-align: center"><br>TL</div><br> |0.0956 |0.0972 |
|<div style="text-align: center"><br>Turkmenistan</div><br> |<div style="text-align: center"><br>TM</div><br> |0.0806 |0.1892 |
|<div style="text-align: center"><br>Tunisia</div><br> |<div style="text-align: center"><br>TN</div><br> |0.128 |0.3477 |
|<div style="text-align: center"><br>Tonga</div><br> |<div style="text-align: center"><br>TO</div><br> |0.0733 |0.1064 |
|<div style="text-align: center"><br>Turkey</div><br> |<div style="text-align: center"><br>TR</div><br> |0.0014 |0.0014 |
|<div style="text-align: center"><br>Trinidad and Tobago</div><br> |<div style="text-align: center"><br>TT</div><br> |0.0757 |0.1363 |
|<div style="text-align: center"><br>Tuvalu</div><br> |<div style="text-align: center"><br>TV</div><br> |0.0359 |0.0464 |
|<div style="text-align: center"><br>Taiwan</div><br> |<div style="text-align: center"><br>TW</div><br> |0.0375 |0.0375 |
|<div style="text-align: center"><br>Tanzania</div><br> |<div style="text-align: center"><br>TZ</div><br> |0.0593 |0.2642 |
|<div style="text-align: center"><br>Ukraine</div><br> |<div style="text-align: center"><br>UA</div><br> |0.118 |0.1598 |
|<div style="text-align: center"><br>Uganda</div><br> |<div style="text-align: center"><br>UG</div><br> |0.0873 |0.2202 |
|<div style="text-align: center"><br>United States</div><br> |<div style="text-align: center"><br>US</div><br> |0.0078 |0.0082 |
|<div style="text-align: center"><br>Uruguay</div><br> |<div style="text-align: center"><br>UY</div><br> |0.0363 |0.0501 |
|<div style="text-align: center"><br>Uzbekistan</div><br> |<div style="text-align: center"><br>UZ</div><br> |0.107 |0.4009 |
|<div style="text-align: center"><br>Vatican</div><br> |<div style="text-align: center"><br>VA</div><br> |0.1107 |0.1164 |
|<div style="text-align: center"><br>Saint Vincent and the Grenadines</div><br> |<div style="text-align: center"><br>VC</div><br> |0.0922 |0.1041 |
|<div style="text-align: center"><br>Venezuela</div><br> |<div style="text-align: center"><br>VE</div><br> |0.0579 |0.0919 |
|<div style="text-align: center"><br>The British Virgin Islands</div><br> |<div style="text-align: center"><br>VG</div><br> |0.0911 |0.065 |
|<div style="text-align: center"><br>United States Virgin Islands</div><br> |<div style="text-align: center"><br>VI</div><br> |0.0054 |0.137 |
|<div style="text-align: center"><br>Vietnam</div><br> |<div style="text-align: center"><br>VN</div><br> |0.0404 |0.1294 |
|<div style="text-align: center"><br>Vanuatu</div><br> |<div style="text-align: center"><br>VU</div><br> |0.1072 |0.113 |
|<div style="text-align: center"><br>Wallis and Futuna</div><br> |<div style="text-align: center"><br>WF</div><br> |0.0699 |0.0545 |
|<div style="text-align: center"><br>Samoa</div><br> |<div style="text-align: center"><br>WS</div><br> |0.1059 |0.1294 |
|<div style="text-align: center"><br>Kosovo</div><br> |<div style="text-align: center"><br>XK</div><br> |0.1264 |0.2141 |
|<div style="text-align: center"><br>Yemen</div><br> |<div style="text-align: center"><br>YE</div><br> |0.1591 |0.2358 |
|<div style="text-align: center"><br>Mayotte</div><br> |<div style="text-align: center"><br>YT</div><br> |0.0853 |0.0703 |
|<div style="text-align: center"><br>South Africa</div><br> |<div style="text-align: center"><br>ZA</div><br> |0.0142 |0.0605 |
|<div style="text-align: center"><br>Zambia</div><br> |<div style="text-align: center"><br>ZM</div><br> |0.0766 |0.2438 |
|<div style="text-align: center"><br>Zimbabwe</div><br> |<div style="text-align: center"><br>ZW</div><br> |0.0623 |0.1155 |
