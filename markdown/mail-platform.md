<!-- .slide: data-state="section-break" id="section-break-1" data-timing="10s" -->
# TelekomMail Platform


<!-- .slide: data-state="normal" id="telekommail" data-timing="20s" data-menu-title="TelekomMail" -->
## TelekomMail

* DT's mail platform for customers <!-- .element class="fragment" data-fragment-index="1"-->
  * includes also voice mail files <!-- .element class="fragment" data-fragment-index="1"-->
* dovecot <!-- .element class="fragment" data-fragment-index="2"-->
* NAS with sharded NFS <!-- .element class="fragment" data-fragment-index="3"-->
* ~39 million accounts <!-- .element class="fragment" data-fragment-index="5"-->
* ~1.3 petabyte net storage <!-- .element class="fragment" data-fragment-index="6"-->
  * ~6.7 billion emails <!-- .element class="fragment" data-fragment-index="7"-->
  * ~1.2 billion index/cache/metadata files <!-- .element class="fragment" data-fragment-index="8"-->
  * ~42% usable raw space <!-- .element class="fragment" data-fragment-index="9"-->

Note: 
- NFS with multiple RAID arrays
- emails are stored compressed


<!-- Slide -->
##### Email Size Distribution
<canvas data-chart="bar">
<!--
{
 "data" : {
     "labels": ["<1k", "<5k", "<10k", "<50k", "<100k", "<500k", "<1m", "<50m", "<100m", ">100m"],

     "datasets": [
         {
	     "data": [9, 227, 80, 356, 157, 140, 16, 28, 0.007, 0.001],
	     "backgroundColor": [
	     	"rgba(166, 206, 227, 0.3)",
		"rgba(31, 120, 180, 0.3)",
		"rgba(178, 223, 138, 0.3)",
		"rgba(51, 160, 44, 0.3)",
		"rgba(251, 154, 153, 0.3)",
		"rgba(227, 26, 28, 0.3)",
		"rgba(253, 191, 111, 0.3)",
		"rgba(255, 127, 0, 0.3)",
		"rgba(202, 178, 214, 0.3)"]
         }
     ]
 },
 "options": {
     "animateScale": "true",
     "responsive": "true",
     "legend": {
           "display": 0
     },
     "plugins": {
     	"datalabels": {
	   "align": "end",
	   "anchor": "end",
	   "display": 1
	}
     },
     "scales": {
            "yAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	},
                "ticks": {
                    "display": 0
                },
		"scaleLabel": {
       		    "display": 1,
        	    "labelString": "number of emails in million"
      		}
            }],
            "xAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	}
            }]
        }
 }
}
-->
</canvas>

Note: emails over 50m very likely via IMAP, never sent


<!-- Slide -->
##### NFS Operations
<canvas data-chart="bar">
<!--
{
 "data" : {
     "labels": ["GETATTR", "ACCESS", "LOOKUP", "WRITE", "READ", "SETATTR", "RENAME", "REMOVE", "CREATE"],
     "datasets": [
         {
             "data": [28, 20, 15, 13, 8, 5, 3, 2, 1],
	     "backgroundColor": [
	     	"rgba(166, 206, 227, 0.3)",
		"rgba(31, 120, 180, 0.3)",
		"rgba(178, 223, 138, 0.3)",
		"rgba(51, 160, 44, 0.3)",
		"rgba(251, 154, 153, 0.3)",
		"rgba(227, 26, 28, 0.3)",
		"rgba(253, 191, 111, 0.3)",
		"rgba(255, 127, 0, 0.3)",
		"rgba(202, 178, 214, 0.3)"]
         }
     ]
 },
 "options": {
     "animateScale": "true",
     "responsive": "true",
     "legend": {
           "display": 0
     },
     "plugins": {
     	"datalabels": {
	   "align": "end",
	   "anchor": "end"
	}
     },
     "scales": {
            "yAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	},
                "ticks": {
                    "display": 0
                }
            }],
            "xAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	}
            }]
        }
 }
}
-->
</canvas>


<!-- Slide -->
##### NFS Operations
<canvas data-chart="bar">
<!--
{
 "data" : {
     "labels": ["GETATTR", "ACCESS", "LOOKUP", "WRITE", "READ", "SETATTR", "RENAME", "REMOVE", "CREATE"],
     "datasets": [
         {
             "data": [28, 20, 15, 13, 8, 5, 3, 2, 1],
             "backgroundColor": [ 
	     	"rgba(186, 186, 186, 0.2)",
	     	"rgba(186, 186, 186, 0.2)",
	     	"rgba(186, 186, 186, 0.2)",
	        "rgba(51, 160, 44, 0.6)",
	        "rgba(251, 154, 153, 0.6)",
	     	"rgba(186, 186, 186, 0.2)",
	     	"rgba(186, 186, 186, 0.2)",
	     	"rgba(186, 186, 186, 0.2)"]
         }
     ]
 },
 "options": {
     "animateScale": "true",
     "responsive": "true",
     "legend": {
           "display": 0
     },
     "plugins": {
     	"datalabels": {
	   "align": "end",
	   "anchor": "end"
	}
     },
     "scales": {
            "yAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	},
                "ticks": {
                    "display": 0
                }
            }],
            "xAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	}
            }]
        }
 }
}
-->
</canvas>


<!-- Slide -->
##### NFS Traffic
<canvas data-chart="bar">
<!--
{
 "data" : {
     "labels": ["GETATTR", "ACCESS", "LOOKUP", "WRITE", "READ", "SETATTR", "RENAME", "REMOVE", "CREATE"],
     "datasets": [
         {
             "data": [0.8 , 0.7 , 0.6 , 57.9 , 39.1 , 0.2 , 0.2 , 0.1, 0.1 ],
	     "backgroundColor": [
	     	"rgba(166, 206, 227, 0.3)",
		"rgba(31, 120, 180, 0.3)",
		"rgba(178, 223, 138, 0.3)",
		"rgba(51, 160, 44, 0.3)",
		"rgba(251, 154, 153, 0.3)",
		"rgba(227, 26, 28, 0.3)",
		"rgba(253, 191, 111, 0.3)",
		"rgba(255, 127, 0, 0.3)",
		"rgba(202, 178, 214, 0.3)"]
         }
     ]
 },
 "options": {
     "animateScale": "true",
     "responsive": "true",
     "legend": {
           "display": 0
     },
     "layout": {
            "padding": {
                "left": 0,
                "right": 0,
                "top": 10,
                "bottom": 0
            }
     },
     "plugins": {
     	"datalabels": {
	   "align": "end",
	   "anchor": "end"
	}
     },
     "scales": {
            "yAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	},
                "ticks": {
                    "display": 0
                }
            }],
            "xAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	}
            }]
        }
 }
}
-->
</canvas>


<!-- Slide -->
##### Relevant IOPs
<canvas data-chart="bar">
<!--
{
 "data" : {
     "labels": ["max (TOTAL/WRITE/READ)", "avg (TOTAL/WRITE/READ)"],
     "datasets": [{
             "data": [835000, 390000],
	     "backgroundColor": [ "rgba(166, 206, 227, 0.3)",
	     			  "rgba(166, 206, 227, 0.3)" ]
         }, {
             "data": [108000, 50000],
	     "backgroundColor": ["rgba(31, 120, 180, 0.3)",
	                         "rgba(31, 120, 180, 0.3)" ]
         }, {
             "data": [66000, 31000],
	     "backgroundColor": ["rgba(202, 178, 214, 0.3)",
	                         "rgba(202, 178, 214, 0.3)" ]
	 }
     ]
 },
 "options": {
     "animateScale": "true",
     "responsive": "true",
     "legend": {
           "display": 0
     },
     "layout": {
            "padding": {
                "left": 0,
                "right": 0,
                "top": 10,
                "bottom": 0
            }
     },
     "plugins": {
     	"datalabels": {
	   "align": "end",
	   "anchor": "end"
	}
     },
     "scales": {
            "yAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	},
                "ticks": {
                    "display": 0
                }
            }],
            "xAxes": [{
	    	"gridLines": {
                    "color": "rgba(0, 0, 0, 0)"
            	}
            }]
        }
 }
}
-->
</canvas>


<!-- .slide: data-state="normal" id="store-emails" data-timing="20s" data-menu-title="How stored?" -->
## How are emails stored?

* WORM <!-- .element class="fragment" data-fragment-index="0"-->
* mailbox, maildir, DB <!-- .element class="fragment" data-fragment-index="1"-->
* usually separated metadata, caches and indexes <!-- .element class="fragment" data-fragment-index="2"-->
  * lost of metadata/indexes is critical <!-- .element class="fragment" data-fragment-index="2"-->
* without attachments easy to compress <!-- .element class="fragment" data-fragment-index="3"-->
* attachments may  deduplicated <!-- .element class="fragment" data-fragment-index="4"-->

Note: 
- Emails are written once, read many ; 
- lost/damage of metadata/indexes need reconstruction of user mailboxes, may be possible, but no folders and info about e.g read/forward/replied
- deduplication can be a legal decision, DT doesn't do it atm.


<!-- .slide: data-state="normal" id="store-emails" data-timing="20s" data-menu-title="How stored?" -->
## Storage

* load pattern depends on: <!-- .element class="fragment" data-fragment-index="0"-->
  * protocol (IMAP vs POP3) <!-- .element class="fragment" data-fragment-index="0"-->
  * user frontend (mailer vs webmailer) <!-- .element class="fragment" data-fragment-index="0"-->
  * mail server implementation <!-- .element class="fragment" data-fragment-index="0"-->
* storage type depends on: <!-- .element class="fragment" data-fragment-index="1"-->
  * sync between workers <!-- .element class="fragment" data-fragment-index="1"-->
  * plugins <!-- .element class="fragment" data-fragment-index="1"-->
  * snapshots <!-- .element class="fragment" data-fragment-index="1"-->

Note: TODO: refine


<!-- .slide: data-state="normal" id="project-motivation" data-timing="20s" data-menu-title="Project Motivation" -->
## Motivation

* faster and automatic self healing <!-- .element class="fragment" data-fragment-index="1"-->
* less IO overhead <!-- .element class="fragment" data-fragment-index="2"-->
* prevent vendor lock-in <!-- .element class="fragment" data-fragment-index="3"-->
* commodity hardware <!-- .element class="fragment" data-fragment-index="4"-->
* open source where feasible <!-- .element class="fragment" data-fragment-index="5"-->
* reduce Total Cost of Ownership <!-- .element class="fragment" data-fragment-index="6"-->

Note: 
- self healing: compared to sharded RAID setups
- overhead: compared to NFS getattr/access/lookups
- TOC: nice to have but very likely not possible within the first years due to required training and support
