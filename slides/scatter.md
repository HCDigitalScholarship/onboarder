<!-- some code adapted from www.degeneratestate.org/static/metal_lyrics/metal_line.html -->
<!-- <!DOCTYPE html>
<meta content="utf-8"> -->
<style> /* set the CSS */

body {
  font: 12px Arial;
}

svg {
  font: 12px Helvetica;
}

path {
  stroke: steelblue;
  stroke-width: 2;
  fill: none;
}

.grid line {
  stroke: lightgrey;
  stroke-opacity: 0.4;
  shape-rendering: crispEdges;
}

.grid path {
  stroke-width: 0;
}

.axis path,
.axis lineper {
  fill: none;
  stroke: grey;
  stroke-width: 1;
  shape-rendering: crispEdges;
}

div.tooltip {
  position: absolute;
  text-align: center;
  width: 150px;
  height: 28px;
  padding: 2px;
  font: 12px sans-serif;
  background: lightsteelblue;
  border: 0px;
  border-radius: 8px;
  pointer-events: none;
}

div.tooltipscore {
  position: absolute;
  text-align: center;
  width: 150px;
  height: 50px;
  padding: 2px;
  font: 10px sans-serif;
  background: lightsteelblue;
  border: 0px;
  border-radius: 8px;
  pointer-events: none;
}

.category_header {
  font: 12px sans-serif;
  font-weight: bolder;
  text-decoration: underline;
}

div.label {
  color: rgb(252, 251, 253);
  color: rgb(63, 0, 125);
  color: rgb(158, 155, 201);

  position: absolute;
  text-align: left;
  padding: 1px;
  border-spacing: 1px;
  font: 10px sans-serif;
  font-family: Sans-Serif;
  border: 0;
  pointer-events: none;
}
/*
input {
  border: 1px dotted #ccc;
  background: white;
  font-family: monospace;
  padding: 10px 20px;
  font-size: 14px;
  margin: 20px 10px 30px 0;
  color: darkred;
}*/

.alert {
  font-family: monospace;
  padding: 10px 20px;
  font-size: 14px;
  margin: 20px 10px 30px 0;
  color: darkred;
}

ul.top_terms li {
  padding-right: 20px;
  font-size: 30pt;
  color: red;
}
/*
input:focus {
  background-color: lightyellow;
  outline: none;
}*/

.snippet {
  padding-bottom: 10px;
  padding-left: 5px;
  padding-right: 5px;
  white-space: pre-wrap;
}

.snippet_header {
  font-size: 20px;
  font-family: Helvetica, Arial, Sans-Serif;
  font-weight: bolder;
  #text-decoration: underline;
  text-align: center;
  border-bottom-width: 10px;
  border-bottom-color: #888888;
  padding-bottom: 10px;
}

.topic_preview {
  font-size: 12px;
  font-family: Helvetica, Arial, Sans-Serif;
  text-align: center;
  padding-bottom: 10px;
  font-weight: normal;
  text-decoration: none;
}


#d3-div-1-categoryinfo {
  font-size: 12px;
  font-family: Helvetica, Arial, Sans-Serif;
  text-align: center;
  padding-bottom: 10px;    

}


#d3-div-1-title-div {
  font-size: 20px;
  font-family: Helvetica, Arial, Sans-Serif;
  text-align: center;
}

.text_header {
  font: 18px sans-serif;
  font-size: 18px;
  font-family: Helvetica, Arial, Sans-Serif;

  font-weight: bolder;
  text-decoration: underline;
  text-align: center;
  color: darkblue;
  padding-bottom: 10px;
}

.text_subheader {
  font-size: 14px;
  font-family: Helvetica, Arial, Sans-Serif;

  text-align: center;
}

.snippet_meta {
  border-top: 3px solid #4588ba;
  font-size: 12px;
  font-family: Helvetica, Arial, Sans-Serif;
  color: darkblue;
}

.not_match {
    background-color: #F0F8FF;
}
    
.contexts {
  width: 45%;
  float: left;
}

.neut_display {
  display: none;
  float: left
}

.scattertext {
  font-size: 10px;
  font-family: Helvetica, Arial, Sans-Serif;
}

.label {
  font-size: 10px;
  font-family: Helvetica, Arial, Sans-Serif;
}

.obscured {
  /*font-size: 14px;
  font-weight: normal;
  color: dimgrey;
  font-family: Helvetica;*/
  text-align: center;
}

.small_label {
  font-size: 10px;
}

#d3-div-1-corpus-stats {
  text-align: center;
}

#d3-div-1-cat {
}

#d3-div-1-notcat {
}

#d3-div-1-neut {
}

#d3-div-1-neutcol {
  display: none;
}
/* Adapted from https://www.w3schools.com/howto/tryit.asp?filename=tryhow_js_autocomplete */

.autocomplete {
  position: relative;
  display: inline-block;
}

input {
  border: 1px solid transparent;
  background-color: #f1f1f1;
  padding: 10px;
  font-size: 16px;
}

input[type=text] {
  background-color: #f1f1f1;
  width: 100%;
}

input[type=submit] {
  background-color: DodgerBlue;
  color: #fff;
  cursor: pointer;
}

.autocomplete-items {
  position: absolute;
  border: 2px solid #d4d4d4;
  border-bottom: none;
  border-top: none;
  z-index: 99;
  /*position the autocomplete items to be the same width as the container:*/
  top: 100%;
  left: 0;
  right: 0;
}

.autocomplete-items div {
  padding: 10px;
  cursor: pointer;
  background-color: #fff;
  border-bottom: 2px solid #d4d4d4;
}

/*when hovering an item:*/
.autocomplete-items div:hover {
  background-color: #e9e9e9;
}

/*when navigating through the items using the arrow keys:*/
.autocomplete-active {
  background-color: DodgerBlue !important;
  color: #ffffff;
}
</style>

<script src="https://cdnjs.cloudflare.com/ajax/libs/d3/4.6.0/d3.min.js" charset="utf-8"></script>
<script src="https://d3js.org/d3-scale-chromatic.v1.min.js" charset="utf-8"></script>

<!-- INSERT SEMIOTIC SQUARE -->
<!--<a onclick="maxFreq = Math.log(data.map(d => d.cat + d.ncat).reduce((a,b) => Math.max(a,b))); plotInterface.redrawPoints(0.1, d => (Math.log(d.ncat + d.cat)/maxFreq), d => d.s, false); plotInterface.redrawPoints(0.1, d => (Math.log(d.ncat + d.cat)/maxFreq), d => d.s, true)">View Score Plot</a>-->
<span id="d3-div-1-title-div"></span>
<div class="scattertext" id="d3-div-1" style="float: left"></div>
<div style="floag: left;">
    <div autocomplete="off">
        <div class="autocomplete">
            <input id="searchInput" type="text" placeholder="Search the chart">
        </div>
    </div>
</div>
<br/>
<div id="d3-div-1-corpus-stats"></div>
<div id="d3-div-1-overlapped-terms"></div>
<a name="d3-div-1-snippets"></a>
<a name="d3-div-1-snippetsalt"></a>
<div id="d3-div-1-termstats"></div>
<div id="d3-div-1-overlapped-terms-clicked"></div>
<div id="d3-div-1-categoryinfo" style="display: hidden"></div>
<div id="d3-div-2">
  <div class="d3-div-1-contexts">
    <div class="snippet_header" id="d3-div-1-cathead"></div>
    <div class="snippet" id="d3-div-1-cat"></div>
  </div>
  <div id="d3-div-1-notcol" class="d3-div-1-contexts">
    <div class="snippet_header" id="d3-div-1-notcathead"></div>
    <div class="snippet" id="d3-div-1-notcat"></div>
  </div>
  <div id="d3-div-1-neutcol" class="d3-div-1-contexts">
    <div class="snippet_header" id="d3-div-1-neuthead"></div>
    <div class="snippet" id="d3-div-1-neut"></div>
  </div>
</div>
<script charset="utf-8">
    // Created using Cozy: github.com/uwplse/cozy
function Rectangle(ax1, ay1, ax2, ay2) {
    this.ax1 = ax1;
    this.ay1 = ay1;
    this.ax2 = ax2;
    this.ay2 = ay2;
    this._left7 = undefined;
    this._right8 = undefined;
    this._parent9 = undefined;
    this._min_ax12 = undefined;
    this._min_ay13 = undefined;
    this._max_ay24 = undefined;
    this._height10 = undefined;
}
function RectangleHolder() {
    this.my_size = 0;
    (this)._root1 = null;
}
RectangleHolder.prototype.size = function () {
    return this.my_size;
};
RectangleHolder.prototype.add = function (x) {
    ++this.my_size;
    var _idx69 = (x).ax2;
    (x)._left7 = null;
    (x)._right8 = null;
    (x)._min_ax12 = (x).ax1;
    (x)._min_ay13 = (x).ay1;
    (x)._max_ay24 = (x).ay2;
    (x)._height10 = 0;
    var _previous70 = null;
    var _current71 = (this)._root1;
    var _is_left72 = false;
    while (!((_current71) == null)) {
        _previous70 = _current71;
        if ((_idx69) < ((_current71).ax2)) {
            _current71 = (_current71)._left7;
            _is_left72 = true;
        } else {
            _current71 = (_current71)._right8;
            _is_left72 = false;
        }
    }
    if ((_previous70) == null) {
        (this)._root1 = x;
    } else {
        (x)._parent9 = _previous70;
        if (_is_left72) {
            (_previous70)._left7 = x;
        } else {
            (_previous70)._right8 = x;
        }
    }
    var _cursor73 = (x)._parent9;
    var _changed74 = true;
    while ((_changed74) && (!((_cursor73) == (null)))) {
        var _old__min_ax1275 = (_cursor73)._min_ax12;
        var _old__min_ay1376 = (_cursor73)._min_ay13;
        var _old__max_ay2477 = (_cursor73)._max_ay24;
        var _old_height78 = (_cursor73)._height10;
        /* _min_ax12 is min of ax1 */
        var _augval79 = (_cursor73).ax1;
        var _child80 = (_cursor73)._left7;
        if (!((_child80) == null)) {
            var _val81 = (_child80)._min_ax12;
            _augval79 = ((_augval79) < (_val81)) ? (_augval79) : (_val81);
        }
        var _child82 = (_cursor73)._right8;
        if (!((_child82) == null)) {
            var _val83 = (_child82)._min_ax12;
            _augval79 = ((_augval79) < (_val83)) ? (_augval79) : (_val83);
        }
        (_cursor73)._min_ax12 = _augval79;
        /* _min_ay13 is min of ay1 */
        var _augval84 = (_cursor73).ay1;
        var _child85 = (_cursor73)._left7;
        if (!((_child85) == null)) {
            var _val86 = (_child85)._min_ay13;
            _augval84 = ((_augval84) < (_val86)) ? (_augval84) : (_val86);
        }
        var _child87 = (_cursor73)._right8;
        if (!((_child87) == null)) {
            var _val88 = (_child87)._min_ay13;
            _augval84 = ((_augval84) < (_val88)) ? (_augval84) : (_val88);
        }
        (_cursor73)._min_ay13 = _augval84;
        /* _max_ay24 is max of ay2 */
        var _augval89 = (_cursor73).ay2;
        var _child90 = (_cursor73)._left7;
        if (!((_child90) == null)) {
            var _val91 = (_child90)._max_ay24;
            _augval89 = ((_augval89) < (_val91)) ? (_val91) : (_augval89);
        }
        var _child92 = (_cursor73)._right8;
        if (!((_child92) == null)) {
            var _val93 = (_child92)._max_ay24;
            _augval89 = ((_augval89) < (_val93)) ? (_val93) : (_augval89);
        }
        (_cursor73)._max_ay24 = _augval89;
        (_cursor73)._height10 = 1 + ((((((_cursor73)._left7) == null) ? (-1) : (((_cursor73)._left7)._height10)) > ((((_cursor73)._right8) == null) ? (-1) : (((_cursor73)._right8)._height10))) ? ((((_cursor73)._left7) == null) ? (-1) : (((_cursor73)._left7)._height10)) : ((((_cursor73)._right8) == null) ? (-1) : (((_cursor73)._right8)._height10)));
        _changed74 = false;
        _changed74 = (_changed74) || (!((_old__min_ax1275) == ((_cursor73)._min_ax12)));
        _changed74 = (_changed74) || (!((_old__min_ay1376) == ((_cursor73)._min_ay13)));
        _changed74 = (_changed74) || (!((_old__max_ay2477) == ((_cursor73)._max_ay24)));
        _changed74 = (_changed74) || (!((_old_height78) == ((_cursor73)._height10)));
        _cursor73 = (_cursor73)._parent9;
    }
    /* rebalance AVL tree */
    var _cursor94 = x;
    var _imbalance95;
    while (!(((_cursor94)._parent9) == null)) {
        _cursor94 = (_cursor94)._parent9;
        (_cursor94)._height10 = 1 + ((((((_cursor94)._left7) == null) ? (-1) : (((_cursor94)._left7)._height10)) > ((((_cursor94)._right8) == null) ? (-1) : (((_cursor94)._right8)._height10))) ? ((((_cursor94)._left7) == null) ? (-1) : (((_cursor94)._left7)._height10)) : ((((_cursor94)._right8) == null) ? (-1) : (((_cursor94)._right8)._height10)));
        _imbalance95 = ((((_cursor94)._left7) == null) ? (-1) : (((_cursor94)._left7)._height10)) - ((((_cursor94)._right8) == null) ? (-1) : (((_cursor94)._right8)._height10));
        if ((_imbalance95) > (1)) {
            if ((((((_cursor94)._left7)._left7) == null) ? (-1) : ((((_cursor94)._left7)._left7)._height10)) < (((((_cursor94)._left7)._right8) == null) ? (-1) : ((((_cursor94)._left7)._right8)._height10))) {
                /* rotate ((_cursor94)._left7)._right8 */
                var _a96 = (_cursor94)._left7;
                var _b97 = (_a96)._right8;
                var _c98 = (_b97)._left7;
                /* replace _a96 with _b97 in (_a96)._parent9 */
                if (!(((_a96)._parent9) == null)) {
                    if ((((_a96)._parent9)._left7) == (_a96)) {
                        ((_a96)._parent9)._left7 = _b97;
                    } else {
                        ((_a96)._parent9)._right8 = _b97;
                    }
                }
                if (!((_b97) == null)) {
                    (_b97)._parent9 = (_a96)._parent9;
                }
                /* replace _c98 with _a96 in _b97 */
                (_b97)._left7 = _a96;
                if (!((_a96) == null)) {
                    (_a96)._parent9 = _b97;
                }
                /* replace _b97 with _c98 in _a96 */
                (_a96)._right8 = _c98;
                if (!((_c98) == null)) {
                    (_c98)._parent9 = _a96;
                }
                /* _min_ax12 is min of ax1 */
                var _augval99 = (_a96).ax1;
                var _child100 = (_a96)._left7;
                if (!((_child100) == null)) {
                    var _val101 = (_child100)._min_ax12;
                    _augval99 = ((_augval99) < (_val101)) ? (_augval99) : (_val101);
                }
                var _child102 = (_a96)._right8;
                if (!((_child102) == null)) {
                    var _val103 = (_child102)._min_ax12;
                    _augval99 = ((_augval99) < (_val103)) ? (_augval99) : (_val103);
                }
                (_a96)._min_ax12 = _augval99;
                /* _min_ay13 is min of ay1 */
                var _augval104 = (_a96).ay1;
                var _child105 = (_a96)._left7;
                if (!((_child105) == null)) {
                    var _val106 = (_child105)._min_ay13;
                    _augval104 = ((_augval104) < (_val106)) ? (_augval104) : (_val106);
                }
                var _child107 = (_a96)._right8;
                if (!((_child107) == null)) {
                    var _val108 = (_child107)._min_ay13;
                    _augval104 = ((_augval104) < (_val108)) ? (_augval104) : (_val108);
                }
                (_a96)._min_ay13 = _augval104;
                /* _max_ay24 is max of ay2 */
                var _augval109 = (_a96).ay2;
                var _child110 = (_a96)._left7;
                if (!((_child110) == null)) {
                    var _val111 = (_child110)._max_ay24;
                    _augval109 = ((_augval109) < (_val111)) ? (_val111) : (_augval109);
                }
                var _child112 = (_a96)._right8;
                if (!((_child112) == null)) {
                    var _val113 = (_child112)._max_ay24;
                    _augval109 = ((_augval109) < (_val113)) ? (_val113) : (_augval109);
                }
                (_a96)._max_ay24 = _augval109;
                (_a96)._height10 = 1 + ((((((_a96)._left7) == null) ? (-1) : (((_a96)._left7)._height10)) > ((((_a96)._right8) == null) ? (-1) : (((_a96)._right8)._height10))) ? ((((_a96)._left7) == null) ? (-1) : (((_a96)._left7)._height10)) : ((((_a96)._right8) == null) ? (-1) : (((_a96)._right8)._height10)));
                /* _min_ax12 is min of ax1 */
                var _augval114 = (_b97).ax1;
                var _child115 = (_b97)._left7;
                if (!((_child115) == null)) {
                    var _val116 = (_child115)._min_ax12;
                    _augval114 = ((_augval114) < (_val116)) ? (_augval114) : (_val116);
                }
                var _child117 = (_b97)._right8;
                if (!((_child117) == null)) {
                    var _val118 = (_child117)._min_ax12;
                    _augval114 = ((_augval114) < (_val118)) ? (_augval114) : (_val118);
                }
                (_b97)._min_ax12 = _augval114;
                /* _min_ay13 is min of ay1 */
                var _augval119 = (_b97).ay1;
                var _child120 = (_b97)._left7;
                if (!((_child120) == null)) {
                    var _val121 = (_child120)._min_ay13;
                    _augval119 = ((_augval119) < (_val121)) ? (_augval119) : (_val121);
                }
                var _child122 = (_b97)._right8;
                if (!((_child122) == null)) {
                    var _val123 = (_child122)._min_ay13;
                    _augval119 = ((_augval119) < (_val123)) ? (_augval119) : (_val123);
                }
                (_b97)._min_ay13 = _augval119;
                /* _max_ay24 is max of ay2 */
                var _augval124 = (_b97).ay2;
                var _child125 = (_b97)._left7;
                if (!((_child125) == null)) {
                    var _val126 = (_child125)._max_ay24;
                    _augval124 = ((_augval124) < (_val126)) ? (_val126) : (_augval124);
                }
                var _child127 = (_b97)._right8;
                if (!((_child127) == null)) {
                    var _val128 = (_child127)._max_ay24;
                    _augval124 = ((_augval124) < (_val128)) ? (_val128) : (_augval124);
                }
                (_b97)._max_ay24 = _augval124;
                (_b97)._height10 = 1 + ((((((_b97)._left7) == null) ? (-1) : (((_b97)._left7)._height10)) > ((((_b97)._right8) == null) ? (-1) : (((_b97)._right8)._height10))) ? ((((_b97)._left7) == null) ? (-1) : (((_b97)._left7)._height10)) : ((((_b97)._right8) == null) ? (-1) : (((_b97)._right8)._height10)));
                if (!(((_b97)._parent9) == null)) {
                    /* _min_ax12 is min of ax1 */
                    var _augval129 = ((_b97)._parent9).ax1;
                    var _child130 = ((_b97)._parent9)._left7;
                    if (!((_child130) == null)) {
                        var _val131 = (_child130)._min_ax12;
                        _augval129 = ((_augval129) < (_val131)) ? (_augval129) : (_val131);
                    }
                    var _child132 = ((_b97)._parent9)._right8;
                    if (!((_child132) == null)) {
                        var _val133 = (_child132)._min_ax12;
                        _augval129 = ((_augval129) < (_val133)) ? (_augval129) : (_val133);
                    }
                    ((_b97)._parent9)._min_ax12 = _augval129;
                    /* _min_ay13 is min of ay1 */
                    var _augval134 = ((_b97)._parent9).ay1;
                    var _child135 = ((_b97)._parent9)._left7;
                    if (!((_child135) == null)) {
                        var _val136 = (_child135)._min_ay13;
                        _augval134 = ((_augval134) < (_val136)) ? (_augval134) : (_val136);
                    }
                    var _child137 = ((_b97)._parent9)._right8;
                    if (!((_child137) == null)) {
                        var _val138 = (_child137)._min_ay13;
                        _augval134 = ((_augval134) < (_val138)) ? (_augval134) : (_val138);
                    }
                    ((_b97)._parent9)._min_ay13 = _augval134;
                    /* _max_ay24 is max of ay2 */
                    var _augval139 = ((_b97)._parent9).ay2;
                    var _child140 = ((_b97)._parent9)._left7;
                    if (!((_child140) == null)) {
                        var _val141 = (_child140)._max_ay24;
                        _augval139 = ((_augval139) < (_val141)) ? (_val141) : (_augval139);
                    }
                    var _child142 = ((_b97)._parent9)._right8;
                    if (!((_child142) == null)) {
                        var _val143 = (_child142)._max_ay24;
                        _augval139 = ((_augval139) < (_val143)) ? (_val143) : (_augval139);
                    }
                    ((_b97)._parent9)._max_ay24 = _augval139;
                    ((_b97)._parent9)._height10 = 1 + (((((((_b97)._parent9)._left7) == null) ? (-1) : ((((_b97)._parent9)._left7)._height10)) > (((((_b97)._parent9)._right8) == null) ? (-1) : ((((_b97)._parent9)._right8)._height10))) ? (((((_b97)._parent9)._left7) == null) ? (-1) : ((((_b97)._parent9)._left7)._height10)) : (((((_b97)._parent9)._right8) == null) ? (-1) : ((((_b97)._parent9)._right8)._height10)));
                } else {
                    (this)._root1 = _b97;
                }
            }
            /* rotate (_cursor94)._left7 */
            var _a144 = _cursor94;
            var _b145 = (_a144)._left7;
            var _c146 = (_b145)._right8;
            /* replace _a144 with _b145 in (_a144)._parent9 */
            if (!(((_a144)._parent9) == null)) {
                if ((((_a144)._parent9)._left7) == (_a144)) {
                    ((_a144)._parent9)._left7 = _b145;
                } else {
                    ((_a144)._parent9)._right8 = _b145;
                }
            }
            if (!((_b145) == null)) {
                (_b145)._parent9 = (_a144)._parent9;
            }
            /* replace _c146 with _a144 in _b145 */
            (_b145)._right8 = _a144;
            if (!((_a144) == null)) {
                (_a144)._parent9 = _b145;
            }
            /* replace _b145 with _c146 in _a144 */
            (_a144)._left7 = _c146;
            if (!((_c146) == null)) {
                (_c146)._parent9 = _a144;
            }
            /* _min_ax12 is min of ax1 */
            var _augval147 = (_a144).ax1;
            var _child148 = (_a144)._left7;
            if (!((_child148) == null)) {
                var _val149 = (_child148)._min_ax12;
                _augval147 = ((_augval147) < (_val149)) ? (_augval147) : (_val149);
            }
            var _child150 = (_a144)._right8;
            if (!((_child150) == null)) {
                var _val151 = (_child150)._min_ax12;
                _augval147 = ((_augval147) < (_val151)) ? (_augval147) : (_val151);
            }
            (_a144)._min_ax12 = _augval147;
            /* _min_ay13 is min of ay1 */
            var _augval152 = (_a144).ay1;
            var _child153 = (_a144)._left7;
            if (!((_child153) == null)) {
                var _val154 = (_child153)._min_ay13;
                _augval152 = ((_augval152) < (_val154)) ? (_augval152) : (_val154);
            }
            var _child155 = (_a144)._right8;
            if (!((_child155) == null)) {
                var _val156 = (_child155)._min_ay13;
                _augval152 = ((_augval152) < (_val156)) ? (_augval152) : (_val156);
            }
            (_a144)._min_ay13 = _augval152;
            /* _max_ay24 is max of ay2 */
            var _augval157 = (_a144).ay2;
            var _child158 = (_a144)._left7;
            if (!((_child158) == null)) {
                var _val159 = (_child158)._max_ay24;
                _augval157 = ((_augval157) < (_val159)) ? (_val159) : (_augval157);
            }
            var _child160 = (_a144)._right8;
            if (!((_child160) == null)) {
                var _val161 = (_child160)._max_ay24;
                _augval157 = ((_augval157) < (_val161)) ? (_val161) : (_augval157);
            }
            (_a144)._max_ay24 = _augval157;
            (_a144)._height10 = 1 + ((((((_a144)._left7) == null) ? (-1) : (((_a144)._left7)._height10)) > ((((_a144)._right8) == null) ? (-1) : (((_a144)._right8)._height10))) ? ((((_a144)._left7) == null) ? (-1) : (((_a144)._left7)._height10)) : ((((_a144)._right8) == null) ? (-1) : (((_a144)._right8)._height10)));
            /* _min_ax12 is min of ax1 */
            var _augval162 = (_b145).ax1;
            var _child163 = (_b145)._left7;
            if (!((_child163) == null)) {
                var _val164 = (_child163)._min_ax12;
                _augval162 = ((_augval162) < (_val164)) ? (_augval162) : (_val164);
            }
            var _child165 = (_b145)._right8;
            if (!((_child165) == null)) {
                var _val166 = (_child165)._min_ax12;
                _augval162 = ((_augval162) < (_val166)) ? (_augval162) : (_val166);
            }
            (_b145)._min_ax12 = _augval162;
            /* _min_ay13 is min of ay1 */
            var _augval167 = (_b145).ay1;
            var _child168 = (_b145)._left7;
            if (!((_child168) == null)) {
                var _val169 = (_child168)._min_ay13;
                _augval167 = ((_augval167) < (_val169)) ? (_augval167) : (_val169);
            }
            var _child170 = (_b145)._right8;
            if (!((_child170) == null)) {
                var _val171 = (_child170)._min_ay13;
                _augval167 = ((_augval167) < (_val171)) ? (_augval167) : (_val171);
            }
            (_b145)._min_ay13 = _augval167;
            /* _max_ay24 is max of ay2 */
            var _augval172 = (_b145).ay2;
            var _child173 = (_b145)._left7;
            if (!((_child173) == null)) {
                var _val174 = (_child173)._max_ay24;
                _augval172 = ((_augval172) < (_val174)) ? (_val174) : (_augval172);
            }
            var _child175 = (_b145)._right8;
            if (!((_child175) == null)) {
                var _val176 = (_child175)._max_ay24;
                _augval172 = ((_augval172) < (_val176)) ? (_val176) : (_augval172);
            }
            (_b145)._max_ay24 = _augval172;
            (_b145)._height10 = 1 + ((((((_b145)._left7) == null) ? (-1) : (((_b145)._left7)._height10)) > ((((_b145)._right8) == null) ? (-1) : (((_b145)._right8)._height10))) ? ((((_b145)._left7) == null) ? (-1) : (((_b145)._left7)._height10)) : ((((_b145)._right8) == null) ? (-1) : (((_b145)._right8)._height10)));
            if (!(((_b145)._parent9) == null)) {
                /* _min_ax12 is min of ax1 */
                var _augval177 = ((_b145)._parent9).ax1;
                var _child178 = ((_b145)._parent9)._left7;
                if (!((_child178) == null)) {
                    var _val179 = (_child178)._min_ax12;
                    _augval177 = ((_augval177) < (_val179)) ? (_augval177) : (_val179);
                }
                var _child180 = ((_b145)._parent9)._right8;
                if (!((_child180) == null)) {
                    var _val181 = (_child180)._min_ax12;
                    _augval177 = ((_augval177) < (_val181)) ? (_augval177) : (_val181);
                }
                ((_b145)._parent9)._min_ax12 = _augval177;
                /* _min_ay13 is min of ay1 */
                var _augval182 = ((_b145)._parent9).ay1;
                var _child183 = ((_b145)._parent9)._left7;
                if (!((_child183) == null)) {
                    var _val184 = (_child183)._min_ay13;
                    _augval182 = ((_augval182) < (_val184)) ? (_augval182) : (_val184);
                }
                var _child185 = ((_b145)._parent9)._right8;
                if (!((_child185) == null)) {
                    var _val186 = (_child185)._min_ay13;
                    _augval182 = ((_augval182) < (_val186)) ? (_augval182) : (_val186);
                }
                ((_b145)._parent9)._min_ay13 = _augval182;
                /* _max_ay24 is max of ay2 */
                var _augval187 = ((_b145)._parent9).ay2;
                var _child188 = ((_b145)._parent9)._left7;
                if (!((_child188) == null)) {
                    var _val189 = (_child188)._max_ay24;
                    _augval187 = ((_augval187) < (_val189)) ? (_val189) : (_augval187);
                }
                var _child190 = ((_b145)._parent9)._right8;
                if (!((_child190) == null)) {
                    var _val191 = (_child190)._max_ay24;
                    _augval187 = ((_augval187) < (_val191)) ? (_val191) : (_augval187);
                }
                ((_b145)._parent9)._max_ay24 = _augval187;
                ((_b145)._parent9)._height10 = 1 + (((((((_b145)._parent9)._left7) == null) ? (-1) : ((((_b145)._parent9)._left7)._height10)) > (((((_b145)._parent9)._right8) == null) ? (-1) : ((((_b145)._parent9)._right8)._height10))) ? (((((_b145)._parent9)._left7) == null) ? (-1) : ((((_b145)._parent9)._left7)._height10)) : (((((_b145)._parent9)._right8) == null) ? (-1) : ((((_b145)._parent9)._right8)._height10)));
            } else {
                (this)._root1 = _b145;
            }
            _cursor94 = (_cursor94)._parent9;
        } else if ((_imbalance95) < (-1)) {
            if ((((((_cursor94)._right8)._left7) == null) ? (-1) : ((((_cursor94)._right8)._left7)._height10)) > (((((_cursor94)._right8)._right8) == null) ? (-1) : ((((_cursor94)._right8)._right8)._height10))) {
                /* rotate ((_cursor94)._right8)._left7 */
                var _a192 = (_cursor94)._right8;
                var _b193 = (_a192)._left7;
                var _c194 = (_b193)._right8;
                /* replace _a192 with _b193 in (_a192)._parent9 */
                if (!(((_a192)._parent9) == null)) {
                    if ((((_a192)._parent9)._left7) == (_a192)) {
                        ((_a192)._parent9)._left7 = _b193;
                    } else {
                        ((_a192)._parent9)._right8 = _b193;
                    }
                }
                if (!((_b193) == null)) {
                    (_b193)._parent9 = (_a192)._parent9;
                }
                /* replace _c194 with _a192 in _b193 */
                (_b193)._right8 = _a192;
                if (!((_a192) == null)) {
                    (_a192)._parent9 = _b193;
                }
                /* replace _b193 with _c194 in _a192 */
                (_a192)._left7 = _c194;
                if (!((_c194) == null)) {
                    (_c194)._parent9 = _a192;
                }
                /* _min_ax12 is min of ax1 */
                var _augval195 = (_a192).ax1;
                var _child196 = (_a192)._left7;
                if (!((_child196) == null)) {
                    var _val197 = (_child196)._min_ax12;
                    _augval195 = ((_augval195) < (_val197)) ? (_augval195) : (_val197);
                }
                var _child198 = (_a192)._right8;
                if (!((_child198) == null)) {
                    var _val199 = (_child198)._min_ax12;
                    _augval195 = ((_augval195) < (_val199)) ? (_augval195) : (_val199);
                }
                (_a192)._min_ax12 = _augval195;
                /* _min_ay13 is min of ay1 */
                var _augval200 = (_a192).ay1;
                var _child201 = (_a192)._left7;
                if (!((_child201) == null)) {
                    var _val202 = (_child201)._min_ay13;
                    _augval200 = ((_augval200) < (_val202)) ? (_augval200) : (_val202);
                }
                var _child203 = (_a192)._right8;
                if (!((_child203) == null)) {
                    var _val204 = (_child203)._min_ay13;
                    _augval200 = ((_augval200) < (_val204)) ? (_augval200) : (_val204);
                }
                (_a192)._min_ay13 = _augval200;
                /* _max_ay24 is max of ay2 */
                var _augval205 = (_a192).ay2;
                var _child206 = (_a192)._left7;
                if (!((_child206) == null)) {
                    var _val207 = (_child206)._max_ay24;
                    _augval205 = ((_augval205) < (_val207)) ? (_val207) : (_augval205);
                }
                var _child208 = (_a192)._right8;
                if (!((_child208) == null)) {
                    var _val209 = (_child208)._max_ay24;
                    _augval205 = ((_augval205) < (_val209)) ? (_val209) : (_augval205);
                }
                (_a192)._max_ay24 = _augval205;
                (_a192)._height10 = 1 + ((((((_a192)._left7) == null) ? (-1) : (((_a192)._left7)._height10)) > ((((_a192)._right8) == null) ? (-1) : (((_a192)._right8)._height10))) ? ((((_a192)._left7) == null) ? (-1) : (((_a192)._left7)._height10)) : ((((_a192)._right8) == null) ? (-1) : (((_a192)._right8)._height10)));
                /* _min_ax12 is min of ax1 */
                var _augval210 = (_b193).ax1;
                var _child211 = (_b193)._left7;
                if (!((_child211) == null)) {
                    var _val212 = (_child211)._min_ax12;
                    _augval210 = ((_augval210) < (_val212)) ? (_augval210) : (_val212);
                }
                var _child213 = (_b193)._right8;
                if (!((_child213) == null)) {
                    var _val214 = (_child213)._min_ax12;
                    _augval210 = ((_augval210) < (_val214)) ? (_augval210) : (_val214);
                }
                (_b193)._min_ax12 = _augval210;
                /* _min_ay13 is min of ay1 */
                var _augval215 = (_b193).ay1;
                var _child216 = (_b193)._left7;
                if (!((_child216) == null)) {
                    var _val217 = (_child216)._min_ay13;
                    _augval215 = ((_augval215) < (_val217)) ? (_augval215) : (_val217);
                }
                var _child218 = (_b193)._right8;
                if (!((_child218) == null)) {
                    var _val219 = (_child218)._min_ay13;
                    _augval215 = ((_augval215) < (_val219)) ? (_augval215) : (_val219);
                }
                (_b193)._min_ay13 = _augval215;
                /* _max_ay24 is max of ay2 */
                var _augval220 = (_b193).ay2;
                var _child221 = (_b193)._left7;
                if (!((_child221) == null)) {
                    var _val222 = (_child221)._max_ay24;
                    _augval220 = ((_augval220) < (_val222)) ? (_val222) : (_augval220);
                }
                var _child223 = (_b193)._right8;
                if (!((_child223) == null)) {
                    var _val224 = (_child223)._max_ay24;
                    _augval220 = ((_augval220) < (_val224)) ? (_val224) : (_augval220);
                }
                (_b193)._max_ay24 = _augval220;
                (_b193)._height10 = 1 + ((((((_b193)._left7) == null) ? (-1) : (((_b193)._left7)._height10)) > ((((_b193)._right8) == null) ? (-1) : (((_b193)._right8)._height10))) ? ((((_b193)._left7) == null) ? (-1) : (((_b193)._left7)._height10)) : ((((_b193)._right8) == null) ? (-1) : (((_b193)._right8)._height10)));
                if (!(((_b193)._parent9) == null)) {
                    /* _min_ax12 is min of ax1 */
                    var _augval225 = ((_b193)._parent9).ax1;
                    var _child226 = ((_b193)._parent9)._left7;
                    if (!((_child226) == null)) {
                        var _val227 = (_child226)._min_ax12;
                        _augval225 = ((_augval225) < (_val227)) ? (_augval225) : (_val227);
                    }
                    var _child228 = ((_b193)._parent9)._right8;
                    if (!((_child228) == null)) {
                        var _val229 = (_child228)._min_ax12;
                        _augval225 = ((_augval225) < (_val229)) ? (_augval225) : (_val229);
                    }
                    ((_b193)._parent9)._min_ax12 = _augval225;
                    /* _min_ay13 is min of ay1 */
                    var _augval230 = ((_b193)._parent9).ay1;
                    var _child231 = ((_b193)._parent9)._left7;
                    if (!((_child231) == null)) {
                        var _val232 = (_child231)._min_ay13;
                        _augval230 = ((_augval230) < (_val232)) ? (_augval230) : (_val232);
                    }
                    var _child233 = ((_b193)._parent9)._right8;
                    if (!((_child233) == null)) {
                        var _val234 = (_child233)._min_ay13;
                        _augval230 = ((_augval230) < (_val234)) ? (_augval230) : (_val234);
                    }
                    ((_b193)._parent9)._min_ay13 = _augval230;
                    /* _max_ay24 is max of ay2 */
                    var _augval235 = ((_b193)._parent9).ay2;
                    var _child236 = ((_b193)._parent9)._left7;
                    if (!((_child236) == null)) {
                        var _val237 = (_child236)._max_ay24;
                        _augval235 = ((_augval235) < (_val237)) ? (_val237) : (_augval235);
                    }
                    var _child238 = ((_b193)._parent9)._right8;
                    if (!((_child238) == null)) {
                        var _val239 = (_child238)._max_ay24;
                        _augval235 = ((_augval235) < (_val239)) ? (_val239) : (_augval235);
                    }
                    ((_b193)._parent9)._max_ay24 = _augval235;
                    ((_b193)._parent9)._height10 = 1 + (((((((_b193)._parent9)._left7) == null) ? (-1) : ((((_b193)._parent9)._left7)._height10)) > (((((_b193)._parent9)._right8) == null) ? (-1) : ((((_b193)._parent9)._right8)._height10))) ? (((((_b193)._parent9)._left7) == null) ? (-1) : ((((_b193)._parent9)._left7)._height10)) : (((((_b193)._parent9)._right8) == null) ? (-1) : ((((_b193)._parent9)._right8)._height10)));
                } else {
                    (this)._root1 = _b193;
                }
            }
            /* rotate (_cursor94)._right8 */
            var _a240 = _cursor94;
            var _b241 = (_a240)._right8;
            var _c242 = (_b241)._left7;
            /* replace _a240 with _b241 in (_a240)._parent9 */
            if (!(((_a240)._parent9) == null)) {
                if ((((_a240)._parent9)._left7) == (_a240)) {
                    ((_a240)._parent9)._left7 = _b241;
                } else {
                    ((_a240)._parent9)._right8 = _b241;
                }
            }
            if (!((_b241) == null)) {
                (_b241)._parent9 = (_a240)._parent9;
            }
            /* replace _c242 with _a240 in _b241 */
            (_b241)._left7 = _a240;
            if (!((_a240) == null)) {
                (_a240)._parent9 = _b241;
            }
            /* replace _b241 with _c242 in _a240 */
            (_a240)._right8 = _c242;
            if (!((_c242) == null)) {
                (_c242)._parent9 = _a240;
            }
            /* _min_ax12 is min of ax1 */
            var _augval243 = (_a240).ax1;
            var _child244 = (_a240)._left7;
            if (!((_child244) == null)) {
                var _val245 = (_child244)._min_ax12;
                _augval243 = ((_augval243) < (_val245)) ? (_augval243) : (_val245);
            }
            var _child246 = (_a240)._right8;
            if (!((_child246) == null)) {
                var _val247 = (_child246)._min_ax12;
                _augval243 = ((_augval243) < (_val247)) ? (_augval243) : (_val247);
            }
            (_a240)._min_ax12 = _augval243;
            /* _min_ay13 is min of ay1 */
            var _augval248 = (_a240).ay1;
            var _child249 = (_a240)._left7;
            if (!((_child249) == null)) {
                var _val250 = (_child249)._min_ay13;
                _augval248 = ((_augval248) < (_val250)) ? (_augval248) : (_val250);
            }
            var _child251 = (_a240)._right8;
            if (!((_child251) == null)) {
                var _val252 = (_child251)._min_ay13;
                _augval248 = ((_augval248) < (_val252)) ? (_augval248) : (_val252);
            }
            (_a240)._min_ay13 = _augval248;
            /* _max_ay24 is max of ay2 */
            var _augval253 = (_a240).ay2;
            var _child254 = (_a240)._left7;
            if (!((_child254) == null)) {
                var _val255 = (_child254)._max_ay24;
                _augval253 = ((_augval253) < (_val255)) ? (_val255) : (_augval253);
            }
            var _child256 = (_a240)._right8;
            if (!((_child256) == null)) {
                var _val257 = (_child256)._max_ay24;
                _augval253 = ((_augval253) < (_val257)) ? (_val257) : (_augval253);
            }
            (_a240)._max_ay24 = _augval253;
            (_a240)._height10 = 1 + ((((((_a240)._left7) == null) ? (-1) : (((_a240)._left7)._height10)) > ((((_a240)._right8) == null) ? (-1) : (((_a240)._right8)._height10))) ? ((((_a240)._left7) == null) ? (-1) : (((_a240)._left7)._height10)) : ((((_a240)._right8) == null) ? (-1) : (((_a240)._right8)._height10)));
            /* _min_ax12 is min of ax1 */
            var _augval258 = (_b241).ax1;
            var _child259 = (_b241)._left7;
            if (!((_child259) == null)) {
                var _val260 = (_child259)._min_ax12;
                _augval258 = ((_augval258) < (_val260)) ? (_augval258) : (_val260);
            }
            var _child261 = (_b241)._right8;
            if (!((_child261) == null)) {
                var _val262 = (_child261)._min_ax12;
                _augval258 = ((_augval258) < (_val262)) ? (_augval258) : (_val262);
            }
            (_b241)._min_ax12 = _augval258;
            /* _min_ay13 is min of ay1 */
            var _augval263 = (_b241).ay1;
            var _child264 = (_b241)._left7;
            if (!((_child264) == null)) {
                var _val265 = (_child264)._min_ay13;
                _augval263 = ((_augval263) < (_val265)) ? (_augval263) : (_val265);
            }
            var _child266 = (_b241)._right8;
            if (!((_child266) == null)) {
                var _val267 = (_child266)._min_ay13;
                _augval263 = ((_augval263) < (_val267)) ? (_augval263) : (_val267);
            }
            (_b241)._min_ay13 = _augval263;
            /* _max_ay24 is max of ay2 */
            var _augval268 = (_b241).ay2;
            var _child269 = (_b241)._left7;
            if (!((_child269) == null)) {
                var _val270 = (_child269)._max_ay24;
                _augval268 = ((_augval268) < (_val270)) ? (_val270) : (_augval268);
            }
            var _child271 = (_b241)._right8;
            if (!((_child271) == null)) {
                var _val272 = (_child271)._max_ay24;
                _augval268 = ((_augval268) < (_val272)) ? (_val272) : (_augval268);
            }
            (_b241)._max_ay24 = _augval268;
            (_b241)._height10 = 1 + ((((((_b241)._left7) == null) ? (-1) : (((_b241)._left7)._height10)) > ((((_b241)._right8) == null) ? (-1) : (((_b241)._right8)._height10))) ? ((((_b241)._left7) == null) ? (-1) : (((_b241)._left7)._height10)) : ((((_b241)._right8) == null) ? (-1) : (((_b241)._right8)._height10)));
            if (!(((_b241)._parent9) == null)) {
                /* _min_ax12 is min of ax1 */
                var _augval273 = ((_b241)._parent9).ax1;
                var _child274 = ((_b241)._parent9)._left7;
                if (!((_child274) == null)) {
                    var _val275 = (_child274)._min_ax12;
                    _augval273 = ((_augval273) < (_val275)) ? (_augval273) : (_val275);
                }
                var _child276 = ((_b241)._parent9)._right8;
                if (!((_child276) == null)) {
                    var _val277 = (_child276)._min_ax12;
                    _augval273 = ((_augval273) < (_val277)) ? (_augval273) : (_val277);
                }
                ((_b241)._parent9)._min_ax12 = _augval273;
                /* _min_ay13 is min of ay1 */
                var _augval278 = ((_b241)._parent9).ay1;
                var _child279 = ((_b241)._parent9)._left7;
                if (!((_child279) == null)) {
                    var _val280 = (_child279)._min_ay13;
                    _augval278 = ((_augval278) < (_val280)) ? (_augval278) : (_val280);
                }
                var _child281 = ((_b241)._parent9)._right8;
                if (!((_child281) == null)) {
                    var _val282 = (_child281)._min_ay13;
                    _augval278 = ((_augval278) < (_val282)) ? (_augval278) : (_val282);
                }
                ((_b241)._parent9)._min_ay13 = _augval278;
                /* _max_ay24 is max of ay2 */
                var _augval283 = ((_b241)._parent9).ay2;
                var _child284 = ((_b241)._parent9)._left7;
                if (!((_child284) == null)) {
                    var _val285 = (_child284)._max_ay24;
                    _augval283 = ((_augval283) < (_val285)) ? (_val285) : (_augval283);
                }
                var _child286 = ((_b241)._parent9)._right8;
                if (!((_child286) == null)) {
                    var _val287 = (_child286)._max_ay24;
                    _augval283 = ((_augval283) < (_val287)) ? (_val287) : (_augval283);
                }
                ((_b241)._parent9)._max_ay24 = _augval283;
                ((_b241)._parent9)._height10 = 1 + (((((((_b241)._parent9)._left7) == null) ? (-1) : ((((_b241)._parent9)._left7)._height10)) > (((((_b241)._parent9)._right8) == null) ? (-1) : ((((_b241)._parent9)._right8)._height10))) ? (((((_b241)._parent9)._left7) == null) ? (-1) : ((((_b241)._parent9)._left7)._height10)) : (((((_b241)._parent9)._right8) == null) ? (-1) : ((((_b241)._parent9)._right8)._height10)));
            } else {
                (this)._root1 = _b241;
            }
            _cursor94 = (_cursor94)._parent9;
        }
    }
};
RectangleHolder.prototype.remove = function (x) {
    --this.my_size;
    var _parent288 = (x)._parent9;
    var _left289 = (x)._left7;
    var _right290 = (x)._right8;
    var _new_x291;
    if (((_left289) == null) && ((_right290) == null)) {
        _new_x291 = null;
        /* replace x with _new_x291 in _parent288 */
        if (!((_parent288) == null)) {
            if (((_parent288)._left7) == (x)) {
                (_parent288)._left7 = _new_x291;
            } else {
                (_parent288)._right8 = _new_x291;
            }
        }
        if (!((_new_x291) == null)) {
            (_new_x291)._parent9 = _parent288;
        }
    } else if ((!((_left289) == null)) && ((_right290) == null)) {
        _new_x291 = _left289;
        /* replace x with _new_x291 in _parent288 */
        if (!((_parent288) == null)) {
            if (((_parent288)._left7) == (x)) {
                (_parent288)._left7 = _new_x291;
            } else {
                (_parent288)._right8 = _new_x291;
            }
        }
        if (!((_new_x291) == null)) {
            (_new_x291)._parent9 = _parent288;
        }
    } else if (((_left289) == null) && (!((_right290) == null))) {
        _new_x291 = _right290;
        /* replace x with _new_x291 in _parent288 */
        if (!((_parent288) == null)) {
            if (((_parent288)._left7) == (x)) {
                (_parent288)._left7 = _new_x291;
            } else {
                (_parent288)._right8 = _new_x291;
            }
        }
        if (!((_new_x291) == null)) {
            (_new_x291)._parent9 = _parent288;
        }
    } else {
        var _root292 = (x)._right8;
        var _x293 = _root292;
        var _descend294 = true;
        var _from_left295 = true;
        while (true) {
            if ((_x293) == null) {
                _x293 = null;
                break;
            }
            if (_descend294) {
                /* too small? */
                if (false) {
                    if ((!(((_x293)._right8) == null)) && (true)) {
                        if ((_x293) == (_root292)) {
                            _root292 = (_x293)._right8;
                        }
                        _x293 = (_x293)._right8;
                    } else if ((_x293) == (_root292)) {
                        _x293 = null;
                        break;
                    } else {
                        _descend294 = false;
                        _from_left295 = (!(((_x293)._parent9) == null)) && ((_x293) == (((_x293)._parent9)._left7));
                        _x293 = (_x293)._parent9;
                    }
                } else if ((!(((_x293)._left7) == null)) && (true)) {
                    _x293 = (_x293)._left7;
                    /* too large? */
                } else if (false) {
                    if ((_x293) == (_root292)) {
                        _x293 = null;
                        break;
                    } else {
                        _descend294 = false;
                        _from_left295 = (!(((_x293)._parent9) == null)) && ((_x293) == (((_x293)._parent9)._left7));
                        _x293 = (_x293)._parent9;
                    }
                    /* node ok? */
                } else if (true) {
                    break;
                } else if ((_x293) == (_root292)) {
                    _root292 = (_x293)._right8;
                    _x293 = (_x293)._right8;
                } else {
                    if ((!(((_x293)._right8) == null)) && (true)) {
                        if ((_x293) == (_root292)) {
                            _root292 = (_x293)._right8;
                        }
                        _x293 = (_x293)._right8;
                    } else {
                        _descend294 = false;
                        _from_left295 = (!(((_x293)._parent9) == null)) && ((_x293) == (((_x293)._parent9)._left7));
                        _x293 = (_x293)._parent9;
                    }
                }
            } else if (_from_left295) {
                if (false) {
                    _x293 = null;
                    break;
                } else if (true) {
                    break;
                } else if ((!(((_x293)._right8) == null)) && (true)) {
                    _descend294 = true;
                    if ((_x293) == (_root292)) {
                        _root292 = (_x293)._right8;
                    }
                    _x293 = (_x293)._right8;
                } else if ((_x293) == (_root292)) {
                    _x293 = null;
                    break;
                } else {
                    _descend294 = false;
                    _from_left295 = (!(((_x293)._parent9) == null)) && ((_x293) == (((_x293)._parent9)._left7));
                    _x293 = (_x293)._parent9;
                }
            } else {
                if ((_x293) == (_root292)) {
                    _x293 = null;
                    break;
                } else {
                    _descend294 = false;
                    _from_left295 = (!(((_x293)._parent9) == null)) && ((_x293) == (((_x293)._parent9)._left7));
                    _x293 = (_x293)._parent9;
                }
            }
        }
        _new_x291 = _x293;
        var _mp296 = (_x293)._parent9;
        var _mr297 = (_x293)._right8;
        /* replace _x293 with _mr297 in _mp296 */
        if (!((_mp296) == null)) {
            if (((_mp296)._left7) == (_x293)) {
                (_mp296)._left7 = _mr297;
            } else {
                (_mp296)._right8 = _mr297;
            }
        }
        if (!((_mr297) == null)) {
            (_mr297)._parent9 = _mp296;
        }
        /* replace x with _x293 in _parent288 */
        if (!((_parent288) == null)) {
            if (((_parent288)._left7) == (x)) {
                (_parent288)._left7 = _x293;
            } else {
                (_parent288)._right8 = _x293;
            }
        }
        if (!((_x293) == null)) {
            (_x293)._parent9 = _parent288;
        }
        /* replace null with _left289 in _x293 */
        (_x293)._left7 = _left289;
        if (!((_left289) == null)) {
            (_left289)._parent9 = _x293;
        }
        /* replace _mr297 with (x)._right8 in _x293 */
        (_x293)._right8 = (x)._right8;
        if (!(((x)._right8) == null)) {
            ((x)._right8)._parent9 = _x293;
        }
        /* _min_ax12 is min of ax1 */
        var _augval298 = (_x293).ax1;
        var _child299 = (_x293)._left7;
        if (!((_child299) == null)) {
            var _val300 = (_child299)._min_ax12;
            _augval298 = ((_augval298) < (_val300)) ? (_augval298) : (_val300);
        }
        var _child301 = (_x293)._right8;
        if (!((_child301) == null)) {
            var _val302 = (_child301)._min_ax12;
            _augval298 = ((_augval298) < (_val302)) ? (_augval298) : (_val302);
        }
        (_x293)._min_ax12 = _augval298;
        /* _min_ay13 is min of ay1 */
        var _augval303 = (_x293).ay1;
        var _child304 = (_x293)._left7;
        if (!((_child304) == null)) {
            var _val305 = (_child304)._min_ay13;
            _augval303 = ((_augval303) < (_val305)) ? (_augval303) : (_val305);
        }
        var _child306 = (_x293)._right8;
        if (!((_child306) == null)) {
            var _val307 = (_child306)._min_ay13;
            _augval303 = ((_augval303) < (_val307)) ? (_augval303) : (_val307);
        }
        (_x293)._min_ay13 = _augval303;
        /* _max_ay24 is max of ay2 */
        var _augval308 = (_x293).ay2;
        var _child309 = (_x293)._left7;
        if (!((_child309) == null)) {
            var _val310 = (_child309)._max_ay24;
            _augval308 = ((_augval308) < (_val310)) ? (_val310) : (_augval308);
        }
        var _child311 = (_x293)._right8;
        if (!((_child311) == null)) {
            var _val312 = (_child311)._max_ay24;
            _augval308 = ((_augval308) < (_val312)) ? (_val312) : (_augval308);
        }
        (_x293)._max_ay24 = _augval308;
        (_x293)._height10 = 1 + ((((((_x293)._left7) == null) ? (-1) : (((_x293)._left7)._height10)) > ((((_x293)._right8) == null) ? (-1) : (((_x293)._right8)._height10))) ? ((((_x293)._left7) == null) ? (-1) : (((_x293)._left7)._height10)) : ((((_x293)._right8) == null) ? (-1) : (((_x293)._right8)._height10)));
        var _cursor313 = _mp296;
        var _changed314 = true;
        while ((_changed314) && (!((_cursor313) == (_parent288)))) {
            var _old__min_ax12315 = (_cursor313)._min_ax12;
            var _old__min_ay13316 = (_cursor313)._min_ay13;
            var _old__max_ay24317 = (_cursor313)._max_ay24;
            var _old_height318 = (_cursor313)._height10;
            /* _min_ax12 is min of ax1 */
            var _augval319 = (_cursor313).ax1;
            var _child320 = (_cursor313)._left7;
            if (!((_child320) == null)) {
                var _val321 = (_child320)._min_ax12;
                _augval319 = ((_augval319) < (_val321)) ? (_augval319) : (_val321);
            }
            var _child322 = (_cursor313)._right8;
            if (!((_child322) == null)) {
                var _val323 = (_child322)._min_ax12;
                _augval319 = ((_augval319) < (_val323)) ? (_augval319) : (_val323);
            }
            (_cursor313)._min_ax12 = _augval319;
            /* _min_ay13 is min of ay1 */
            var _augval324 = (_cursor313).ay1;
            var _child325 = (_cursor313)._left7;
            if (!((_child325) == null)) {
                var _val326 = (_child325)._min_ay13;
                _augval324 = ((_augval324) < (_val326)) ? (_augval324) : (_val326);
            }
            var _child327 = (_cursor313)._right8;
            if (!((_child327) == null)) {
                var _val328 = (_child327)._min_ay13;
                _augval324 = ((_augval324) < (_val328)) ? (_augval324) : (_val328);
            }
            (_cursor313)._min_ay13 = _augval324;
            /* _max_ay24 is max of ay2 */
            var _augval329 = (_cursor313).ay2;
            var _child330 = (_cursor313)._left7;
            if (!((_child330) == null)) {
                var _val331 = (_child330)._max_ay24;
                _augval329 = ((_augval329) < (_val331)) ? (_val331) : (_augval329);
            }
            var _child332 = (_cursor313)._right8;
            if (!((_child332) == null)) {
                var _val333 = (_child332)._max_ay24;
                _augval329 = ((_augval329) < (_val333)) ? (_val333) : (_augval329);
            }
            (_cursor313)._max_ay24 = _augval329;
            (_cursor313)._height10 = 1 + ((((((_cursor313)._left7) == null) ? (-1) : (((_cursor313)._left7)._height10)) > ((((_cursor313)._right8) == null) ? (-1) : (((_cursor313)._right8)._height10))) ? ((((_cursor313)._left7) == null) ? (-1) : (((_cursor313)._left7)._height10)) : ((((_cursor313)._right8) == null) ? (-1) : (((_cursor313)._right8)._height10)));
            _changed314 = false;
            _changed314 = (_changed314) || (!((_old__min_ax12315) == ((_cursor313)._min_ax12)));
            _changed314 = (_changed314) || (!((_old__min_ay13316) == ((_cursor313)._min_ay13)));
            _changed314 = (_changed314) || (!((_old__max_ay24317) == ((_cursor313)._max_ay24)));
            _changed314 = (_changed314) || (!((_old_height318) == ((_cursor313)._height10)));
            _cursor313 = (_cursor313)._parent9;
        }
    }
    var _cursor334 = _parent288;
    var _changed335 = true;
    while ((_changed335) && (!((_cursor334) == (null)))) {
        var _old__min_ax12336 = (_cursor334)._min_ax12;
        var _old__min_ay13337 = (_cursor334)._min_ay13;
        var _old__max_ay24338 = (_cursor334)._max_ay24;
        var _old_height339 = (_cursor334)._height10;
        /* _min_ax12 is min of ax1 */
        var _augval340 = (_cursor334).ax1;
        var _child341 = (_cursor334)._left7;
        if (!((_child341) == null)) {
            var _val342 = (_child341)._min_ax12;
            _augval340 = ((_augval340) < (_val342)) ? (_augval340) : (_val342);
        }
        var _child343 = (_cursor334)._right8;
        if (!((_child343) == null)) {
            var _val344 = (_child343)._min_ax12;
            _augval340 = ((_augval340) < (_val344)) ? (_augval340) : (_val344);
        }
        (_cursor334)._min_ax12 = _augval340;
        /* _min_ay13 is min of ay1 */
        var _augval345 = (_cursor334).ay1;
        var _child346 = (_cursor334)._left7;
        if (!((_child346) == null)) {
            var _val347 = (_child346)._min_ay13;
            _augval345 = ((_augval345) < (_val347)) ? (_augval345) : (_val347);
        }
        var _child348 = (_cursor334)._right8;
        if (!((_child348) == null)) {
            var _val349 = (_child348)._min_ay13;
            _augval345 = ((_augval345) < (_val349)) ? (_augval345) : (_val349);
        }
        (_cursor334)._min_ay13 = _augval345;
        /* _max_ay24 is max of ay2 */
        var _augval350 = (_cursor334).ay2;
        var _child351 = (_cursor334)._left7;
        if (!((_child351) == null)) {
            var _val352 = (_child351)._max_ay24;
            _augval350 = ((_augval350) < (_val352)) ? (_val352) : (_augval350);
        }
        var _child353 = (_cursor334)._right8;
        if (!((_child353) == null)) {
            var _val354 = (_child353)._max_ay24;
            _augval350 = ((_augval350) < (_val354)) ? (_val354) : (_augval350);
        }
        (_cursor334)._max_ay24 = _augval350;
        (_cursor334)._height10 = 1 + ((((((_cursor334)._left7) == null) ? (-1) : (((_cursor334)._left7)._height10)) > ((((_cursor334)._right8) == null) ? (-1) : (((_cursor334)._right8)._height10))) ? ((((_cursor334)._left7) == null) ? (-1) : (((_cursor334)._left7)._height10)) : ((((_cursor334)._right8) == null) ? (-1) : (((_cursor334)._right8)._height10)));
        _changed335 = false;
        _changed335 = (_changed335) || (!((_old__min_ax12336) == ((_cursor334)._min_ax12)));
        _changed335 = (_changed335) || (!((_old__min_ay13337) == ((_cursor334)._min_ay13)));
        _changed335 = (_changed335) || (!((_old__max_ay24338) == ((_cursor334)._max_ay24)));
        _changed335 = (_changed335) || (!((_old_height339) == ((_cursor334)._height10)));
        _cursor334 = (_cursor334)._parent9;
    }
    if (((this)._root1) == (x)) {
        (this)._root1 = _new_x291;
    }
};
RectangleHolder.prototype.updateAx1 = function (__x, new_val) {
    if ((__x).ax1 != new_val) {
        /* _min_ax12 is min of ax1 */
        var _augval355 = new_val;
        var _child356 = (__x)._left7;
        if (!((_child356) == null)) {
            var _val357 = (_child356)._min_ax12;
            _augval355 = ((_augval355) < (_val357)) ? (_augval355) : (_val357);
        }
        var _child358 = (__x)._right8;
        if (!((_child358) == null)) {
            var _val359 = (_child358)._min_ax12;
            _augval355 = ((_augval355) < (_val359)) ? (_augval355) : (_val359);
        }
        (__x)._min_ax12 = _augval355;
        var _cursor360 = (__x)._parent9;
        var _changed361 = true;
        while ((_changed361) && (!((_cursor360) == (null)))) {
            var _old__min_ax12362 = (_cursor360)._min_ax12;
            var _old_height363 = (_cursor360)._height10;
            /* _min_ax12 is min of ax1 */
            var _augval364 = (_cursor360).ax1;
            var _child365 = (_cursor360)._left7;
            if (!((_child365) == null)) {
                var _val366 = (_child365)._min_ax12;
                _augval364 = ((_augval364) < (_val366)) ? (_augval364) : (_val366);
            }
            var _child367 = (_cursor360)._right8;
            if (!((_child367) == null)) {
                var _val368 = (_child367)._min_ax12;
                _augval364 = ((_augval364) < (_val368)) ? (_augval364) : (_val368);
            }
            (_cursor360)._min_ax12 = _augval364;
            (_cursor360)._height10 = 1 + ((((((_cursor360)._left7) == null) ? (-1) : (((_cursor360)._left7)._height10)) > ((((_cursor360)._right8) == null) ? (-1) : (((_cursor360)._right8)._height10))) ? ((((_cursor360)._left7) == null) ? (-1) : (((_cursor360)._left7)._height10)) : ((((_cursor360)._right8) == null) ? (-1) : (((_cursor360)._right8)._height10)));
            _changed361 = false;
            _changed361 = (_changed361) || (!((_old__min_ax12362) == ((_cursor360)._min_ax12)));
            _changed361 = (_changed361) || (!((_old_height363) == ((_cursor360)._height10)));
            _cursor360 = (_cursor360)._parent9;
        }
        (__x).ax1 = new_val;
    }
}
RectangleHolder.prototype.updateAy1 = function (__x, new_val) {
    if ((__x).ay1 != new_val) {
        /* _min_ay13 is min of ay1 */
        var _augval369 = new_val;
        var _child370 = (__x)._left7;
        if (!((_child370) == null)) {
            var _val371 = (_child370)._min_ay13;
            _augval369 = ((_augval369) < (_val371)) ? (_augval369) : (_val371);
        }
        var _child372 = (__x)._right8;
        if (!((_child372) == null)) {
            var _val373 = (_child372)._min_ay13;
            _augval369 = ((_augval369) < (_val373)) ? (_augval369) : (_val373);
        }
        (__x)._min_ay13 = _augval369;
        var _cursor374 = (__x)._parent9;
        var _changed375 = true;
        while ((_changed375) && (!((_cursor374) == (null)))) {
            var _old__min_ay13376 = (_cursor374)._min_ay13;
            var _old_height377 = (_cursor374)._height10;
            /* _min_ay13 is min of ay1 */
            var _augval378 = (_cursor374).ay1;
            var _child379 = (_cursor374)._left7;
            if (!((_child379) == null)) {
                var _val380 = (_child379)._min_ay13;
                _augval378 = ((_augval378) < (_val380)) ? (_augval378) : (_val380);
            }
            var _child381 = (_cursor374)._right8;
            if (!((_child381) == null)) {
                var _val382 = (_child381)._min_ay13;
                _augval378 = ((_augval378) < (_val382)) ? (_augval378) : (_val382);
            }
            (_cursor374)._min_ay13 = _augval378;
            (_cursor374)._height10 = 1 + ((((((_cursor374)._left7) == null) ? (-1) : (((_cursor374)._left7)._height10)) > ((((_cursor374)._right8) == null) ? (-1) : (((_cursor374)._right8)._height10))) ? ((((_cursor374)._left7) == null) ? (-1) : (((_cursor374)._left7)._height10)) : ((((_cursor374)._right8) == null) ? (-1) : (((_cursor374)._right8)._height10)));
            _changed375 = false;
            _changed375 = (_changed375) || (!((_old__min_ay13376) == ((_cursor374)._min_ay13)));
            _changed375 = (_changed375) || (!((_old_height377) == ((_cursor374)._height10)));
            _cursor374 = (_cursor374)._parent9;
        }
        (__x).ay1 = new_val;
    }
}
RectangleHolder.prototype.updateAx2 = function (__x, new_val) {
    if ((__x).ax2 != new_val) {
        var _parent383 = (__x)._parent9;
        var _left384 = (__x)._left7;
        var _right385 = (__x)._right8;
        var _new_x386;
        if (((_left384) == null) && ((_right385) == null)) {
            _new_x386 = null;
            /* replace __x with _new_x386 in _parent383 */
            if (!((_parent383) == null)) {
                if (((_parent383)._left7) == (__x)) {
                    (_parent383)._left7 = _new_x386;
                } else {
                    (_parent383)._right8 = _new_x386;
                }
            }
            if (!((_new_x386) == null)) {
                (_new_x386)._parent9 = _parent383;
            }
        } else if ((!((_left384) == null)) && ((_right385) == null)) {
            _new_x386 = _left384;
            /* replace __x with _new_x386 in _parent383 */
            if (!((_parent383) == null)) {
                if (((_parent383)._left7) == (__x)) {
                    (_parent383)._left7 = _new_x386;
                } else {
                    (_parent383)._right8 = _new_x386;
                }
            }
            if (!((_new_x386) == null)) {
                (_new_x386)._parent9 = _parent383;
            }
        } else if (((_left384) == null) && (!((_right385) == null))) {
            _new_x386 = _right385;
            /* replace __x with _new_x386 in _parent383 */
            if (!((_parent383) == null)) {
                if (((_parent383)._left7) == (__x)) {
                    (_parent383)._left7 = _new_x386;
                } else {
                    (_parent383)._right8 = _new_x386;
                }
            }
            if (!((_new_x386) == null)) {
                (_new_x386)._parent9 = _parent383;
            }
        } else {
            var _root387 = (__x)._right8;
            var _x388 = _root387;
            var _descend389 = true;
            var _from_left390 = true;
            while (true) {
                if ((_x388) == null) {
                    _x388 = null;
                    break;
                }
                if (_descend389) {
                    /* too small? */
                    if (false) {
                        if ((!(((_x388)._right8) == null)) && (true)) {
                            if ((_x388) == (_root387)) {
                                _root387 = (_x388)._right8;
                            }
                            _x388 = (_x388)._right8;
                        } else if ((_x388) == (_root387)) {
                            _x388 = null;
                            break;
                        } else {
                            _descend389 = false;
                            _from_left390 = (!(((_x388)._parent9) == null)) && ((_x388) == (((_x388)._parent9)._left7));
                            _x388 = (_x388)._parent9;
                        }
                    } else if ((!(((_x388)._left7) == null)) && (true)) {
                        _x388 = (_x388)._left7;
                        /* too large? */
                    } else if (false) {
                        if ((_x388) == (_root387)) {
                            _x388 = null;
                            break;
                        } else {
                            _descend389 = false;
                            _from_left390 = (!(((_x388)._parent9) == null)) && ((_x388) == (((_x388)._parent9)._left7));
                            _x388 = (_x388)._parent9;
                        }
                        /* node ok? */
                    } else if (true) {
                        break;
                    } else if ((_x388) == (_root387)) {
                        _root387 = (_x388)._right8;
                        _x388 = (_x388)._right8;
                    } else {
                        if ((!(((_x388)._right8) == null)) && (true)) {
                            if ((_x388) == (_root387)) {
                                _root387 = (_x388)._right8;
                            }
                            _x388 = (_x388)._right8;
                        } else {
                            _descend389 = false;
                            _from_left390 = (!(((_x388)._parent9) == null)) && ((_x388) == (((_x388)._parent9)._left7));
                            _x388 = (_x388)._parent9;
                        }
                    }
                } else if (_from_left390) {
                    if (false) {
                        _x388 = null;
                        break;
                    } else if (true) {
                        break;
                    } else if ((!(((_x388)._right8) == null)) && (true)) {
                        _descend389 = true;
                        if ((_x388) == (_root387)) {
                            _root387 = (_x388)._right8;
                        }
                        _x388 = (_x388)._right8;
                    } else if ((_x388) == (_root387)) {
                        _x388 = null;
                        break;
                    } else {
                        _descend389 = false;
                        _from_left390 = (!(((_x388)._parent9) == null)) && ((_x388) == (((_x388)._parent9)._left7));
                        _x388 = (_x388)._parent9;
                    }
                } else {
                    if ((_x388) == (_root387)) {
                        _x388 = null;
                        break;
                    } else {
                        _descend389 = false;
                        _from_left390 = (!(((_x388)._parent9) == null)) && ((_x388) == (((_x388)._parent9)._left7));
                        _x388 = (_x388)._parent9;
                    }
                }
            }
            _new_x386 = _x388;
            var _mp391 = (_x388)._parent9;
            var _mr392 = (_x388)._right8;
            /* replace _x388 with _mr392 in _mp391 */
            if (!((_mp391) == null)) {
                if (((_mp391)._left7) == (_x388)) {
                    (_mp391)._left7 = _mr392;
                } else {
                    (_mp391)._right8 = _mr392;
                }
            }
            if (!((_mr392) == null)) {
                (_mr392)._parent9 = _mp391;
            }
            /* replace __x with _x388 in _parent383 */
            if (!((_parent383) == null)) {
                if (((_parent383)._left7) == (__x)) {
                    (_parent383)._left7 = _x388;
                } else {
                    (_parent383)._right8 = _x388;
                }
            }
            if (!((_x388) == null)) {
                (_x388)._parent9 = _parent383;
            }
            /* replace null with _left384 in _x388 */
            (_x388)._left7 = _left384;
            if (!((_left384) == null)) {
                (_left384)._parent9 = _x388;
            }
            /* replace _mr392 with (__x)._right8 in _x388 */
            (_x388)._right8 = (__x)._right8;
            if (!(((__x)._right8) == null)) {
                ((__x)._right8)._parent9 = _x388;
            }
            /* _min_ax12 is min of ax1 */
            var _augval393 = (_x388).ax1;
            var _child394 = (_x388)._left7;
            if (!((_child394) == null)) {
                var _val395 = (_child394)._min_ax12;
                _augval393 = ((_augval393) < (_val395)) ? (_augval393) : (_val395);
            }
            var _child396 = (_x388)._right8;
            if (!((_child396) == null)) {
                var _val397 = (_child396)._min_ax12;
                _augval393 = ((_augval393) < (_val397)) ? (_augval393) : (_val397);
            }
            (_x388)._min_ax12 = _augval393;
            /* _min_ay13 is min of ay1 */
            var _augval398 = (_x388).ay1;
            var _child399 = (_x388)._left7;
            if (!((_child399) == null)) {
                var _val400 = (_child399)._min_ay13;
                _augval398 = ((_augval398) < (_val400)) ? (_augval398) : (_val400);
            }
            var _child401 = (_x388)._right8;
            if (!((_child401) == null)) {
                var _val402 = (_child401)._min_ay13;
                _augval398 = ((_augval398) < (_val402)) ? (_augval398) : (_val402);
            }
            (_x388)._min_ay13 = _augval398;
            /* _max_ay24 is max of ay2 */
            var _augval403 = (_x388).ay2;
            var _child404 = (_x388)._left7;
            if (!((_child404) == null)) {
                var _val405 = (_child404)._max_ay24;
                _augval403 = ((_augval403) < (_val405)) ? (_val405) : (_augval403);
            }
            var _child406 = (_x388)._right8;
            if (!((_child406) == null)) {
                var _val407 = (_child406)._max_ay24;
                _augval403 = ((_augval403) < (_val407)) ? (_val407) : (_augval403);
            }
            (_x388)._max_ay24 = _augval403;
            (_x388)._height10 = 1 + ((((((_x388)._left7) == null) ? (-1) : (((_x388)._left7)._height10)) > ((((_x388)._right8) == null) ? (-1) : (((_x388)._right8)._height10))) ? ((((_x388)._left7) == null) ? (-1) : (((_x388)._left7)._height10)) : ((((_x388)._right8) == null) ? (-1) : (((_x388)._right8)._height10)));
            var _cursor408 = _mp391;
            var _changed409 = true;
            while ((_changed409) && (!((_cursor408) == (_parent383)))) {
                var _old__min_ax12410 = (_cursor408)._min_ax12;
                var _old__min_ay13411 = (_cursor408)._min_ay13;
                var _old__max_ay24412 = (_cursor408)._max_ay24;
                var _old_height413 = (_cursor408)._height10;
                /* _min_ax12 is min of ax1 */
                var _augval414 = (_cursor408).ax1;
                var _child415 = (_cursor408)._left7;
                if (!((_child415) == null)) {
                    var _val416 = (_child415)._min_ax12;
                    _augval414 = ((_augval414) < (_val416)) ? (_augval414) : (_val416);
                }
                var _child417 = (_cursor408)._right8;
                if (!((_child417) == null)) {
                    var _val418 = (_child417)._min_ax12;
                    _augval414 = ((_augval414) < (_val418)) ? (_augval414) : (_val418);
                }
                (_cursor408)._min_ax12 = _augval414;
                /* _min_ay13 is min of ay1 */
                var _augval419 = (_cursor408).ay1;
                var _child420 = (_cursor408)._left7;
                if (!((_child420) == null)) {
                    var _val421 = (_child420)._min_ay13;
                    _augval419 = ((_augval419) < (_val421)) ? (_augval419) : (_val421);
                }
                var _child422 = (_cursor408)._right8;
                if (!((_child422) == null)) {
                    var _val423 = (_child422)._min_ay13;
                    _augval419 = ((_augval419) < (_val423)) ? (_augval419) : (_val423);
                }
                (_cursor408)._min_ay13 = _augval419;
                /* _max_ay24 is max of ay2 */
                var _augval424 = (_cursor408).ay2;
                var _child425 = (_cursor408)._left7;
                if (!((_child425) == null)) {
                    var _val426 = (_child425)._max_ay24;
                    _augval424 = ((_augval424) < (_val426)) ? (_val426) : (_augval424);
                }
                var _child427 = (_cursor408)._right8;
                if (!((_child427) == null)) {
                    var _val428 = (_child427)._max_ay24;
                    _augval424 = ((_augval424) < (_val428)) ? (_val428) : (_augval424);
                }
                (_cursor408)._max_ay24 = _augval424;
                (_cursor408)._height10 = 1 + ((((((_cursor408)._left7) == null) ? (-1) : (((_cursor408)._left7)._height10)) > ((((_cursor408)._right8) == null) ? (-1) : (((_cursor408)._right8)._height10))) ? ((((_cursor408)._left7) == null) ? (-1) : (((_cursor408)._left7)._height10)) : ((((_cursor408)._right8) == null) ? (-1) : (((_cursor408)._right8)._height10)));
                _changed409 = false;
                _changed409 = (_changed409) || (!((_old__min_ax12410) == ((_cursor408)._min_ax12)));
                _changed409 = (_changed409) || (!((_old__min_ay13411) == ((_cursor408)._min_ay13)));
                _changed409 = (_changed409) || (!((_old__max_ay24412) == ((_cursor408)._max_ay24)));
                _changed409 = (_changed409) || (!((_old_height413) == ((_cursor408)._height10)));
                _cursor408 = (_cursor408)._parent9;
            }
        }
        var _cursor429 = _parent383;
        var _changed430 = true;
        while ((_changed430) && (!((_cursor429) == (null)))) {
            var _old__min_ax12431 = (_cursor429)._min_ax12;
            var _old__min_ay13432 = (_cursor429)._min_ay13;
            var _old__max_ay24433 = (_cursor429)._max_ay24;
            var _old_height434 = (_cursor429)._height10;
            /* _min_ax12 is min of ax1 */
            var _augval435 = (_cursor429).ax1;
            var _child436 = (_cursor429)._left7;
            if (!((_child436) == null)) {
                var _val437 = (_child436)._min_ax12;
                _augval435 = ((_augval435) < (_val437)) ? (_augval435) : (_val437);
            }
            var _child438 = (_cursor429)._right8;
            if (!((_child438) == null)) {
                var _val439 = (_child438)._min_ax12;
                _augval435 = ((_augval435) < (_val439)) ? (_augval435) : (_val439);
            }
            (_cursor429)._min_ax12 = _augval435;
            /* _min_ay13 is min of ay1 */
            var _augval440 = (_cursor429).ay1;
            var _child441 = (_cursor429)._left7;
            if (!((_child441) == null)) {
                var _val442 = (_child441)._min_ay13;
                _augval440 = ((_augval440) < (_val442)) ? (_augval440) : (_val442);
            }
            var _child443 = (_cursor429)._right8;
            if (!((_child443) == null)) {
                var _val444 = (_child443)._min_ay13;
                _augval440 = ((_augval440) < (_val444)) ? (_augval440) : (_val444);
            }
            (_cursor429)._min_ay13 = _augval440;
            /* _max_ay24 is max of ay2 */
            var _augval445 = (_cursor429).ay2;
            var _child446 = (_cursor429)._left7;
            if (!((_child446) == null)) {
                var _val447 = (_child446)._max_ay24;
                _augval445 = ((_augval445) < (_val447)) ? (_val447) : (_augval445);
            }
            var _child448 = (_cursor429)._right8;
            if (!((_child448) == null)) {
                var _val449 = (_child448)._max_ay24;
                _augval445 = ((_augval445) < (_val449)) ? (_val449) : (_augval445);
            }
            (_cursor429)._max_ay24 = _augval445;
            (_cursor429)._height10 = 1 + ((((((_cursor429)._left7) == null) ? (-1) : (((_cursor429)._left7)._height10)) > ((((_cursor429)._right8) == null) ? (-1) : (((_cursor429)._right8)._height10))) ? ((((_cursor429)._left7) == null) ? (-1) : (((_cursor429)._left7)._height10)) : ((((_cursor429)._right8) == null) ? (-1) : (((_cursor429)._right8)._height10)));
            _changed430 = false;
            _changed430 = (_changed430) || (!((_old__min_ax12431) == ((_cursor429)._min_ax12)));
            _changed430 = (_changed430) || (!((_old__min_ay13432) == ((_cursor429)._min_ay13)));
            _changed430 = (_changed430) || (!((_old__max_ay24433) == ((_cursor429)._max_ay24)));
            _changed430 = (_changed430) || (!((_old_height434) == ((_cursor429)._height10)));
            _cursor429 = (_cursor429)._parent9;
        }
        if (((this)._root1) == (__x)) {
            (this)._root1 = _new_x386;
        }
        (__x)._left7 = null;
        (__x)._right8 = null;
        (__x)._min_ax12 = (__x).ax1;
        (__x)._min_ay13 = (__x).ay1;
        (__x)._max_ay24 = (__x).ay2;
        (__x)._height10 = 0;
        var _previous450 = null;
        var _current451 = (this)._root1;
        var _is_left452 = false;
        while (!((_current451) == null)) {
            _previous450 = _current451;
            if ((new_val) < ((_current451).ax2)) {
                _current451 = (_current451)._left7;
                _is_left452 = true;
            } else {
                _current451 = (_current451)._right8;
                _is_left452 = false;
            }
        }
        if ((_previous450) == null) {
            (this)._root1 = __x;
        } else {
            (__x)._parent9 = _previous450;
            if (_is_left452) {
                (_previous450)._left7 = __x;
            } else {
                (_previous450)._right8 = __x;
            }
        }
        var _cursor453 = (__x)._parent9;
        var _changed454 = true;
        while ((_changed454) && (!((_cursor453) == (null)))) {
            var _old__min_ax12455 = (_cursor453)._min_ax12;
            var _old__min_ay13456 = (_cursor453)._min_ay13;
            var _old__max_ay24457 = (_cursor453)._max_ay24;
            var _old_height458 = (_cursor453)._height10;
            /* _min_ax12 is min of ax1 */
            var _augval459 = (_cursor453).ax1;
            var _child460 = (_cursor453)._left7;
            if (!((_child460) == null)) {
                var _val461 = (_child460)._min_ax12;
                _augval459 = ((_augval459) < (_val461)) ? (_augval459) : (_val461);
            }
            var _child462 = (_cursor453)._right8;
            if (!((_child462) == null)) {
                var _val463 = (_child462)._min_ax12;
                _augval459 = ((_augval459) < (_val463)) ? (_augval459) : (_val463);
            }
            (_cursor453)._min_ax12 = _augval459;
            /* _min_ay13 is min of ay1 */
            var _augval464 = (_cursor453).ay1;
            var _child465 = (_cursor453)._left7;
            if (!((_child465) == null)) {
                var _val466 = (_child465)._min_ay13;
                _augval464 = ((_augval464) < (_val466)) ? (_augval464) : (_val466);
            }
            var _child467 = (_cursor453)._right8;
            if (!((_child467) == null)) {
                var _val468 = (_child467)._min_ay13;
                _augval464 = ((_augval464) < (_val468)) ? (_augval464) : (_val468);
            }
            (_cursor453)._min_ay13 = _augval464;
            /* _max_ay24 is max of ay2 */
            var _augval469 = (_cursor453).ay2;
            var _child470 = (_cursor453)._left7;
            if (!((_child470) == null)) {
                var _val471 = (_child470)._max_ay24;
                _augval469 = ((_augval469) < (_val471)) ? (_val471) : (_augval469);
            }
            var _child472 = (_cursor453)._right8;
            if (!((_child472) == null)) {
                var _val473 = (_child472)._max_ay24;
                _augval469 = ((_augval469) < (_val473)) ? (_val473) : (_augval469);
            }
            (_cursor453)._max_ay24 = _augval469;
            (_cursor453)._height10 = 1 + ((((((_cursor453)._left7) == null) ? (-1) : (((_cursor453)._left7)._height10)) > ((((_cursor453)._right8) == null) ? (-1) : (((_cursor453)._right8)._height10))) ? ((((_cursor453)._left7) == null) ? (-1) : (((_cursor453)._left7)._height10)) : ((((_cursor453)._right8) == null) ? (-1) : (((_cursor453)._right8)._height10)));
            _changed454 = false;
            _changed454 = (_changed454) || (!((_old__min_ax12455) == ((_cursor453)._min_ax12)));
            _changed454 = (_changed454) || (!((_old__min_ay13456) == ((_cursor453)._min_ay13)));
            _changed454 = (_changed454) || (!((_old__max_ay24457) == ((_cursor453)._max_ay24)));
            _changed454 = (_changed454) || (!((_old_height458) == ((_cursor453)._height10)));
            _cursor453 = (_cursor453)._parent9;
        }
        /* rebalance AVL tree */
        var _cursor474 = __x;
        var _imbalance475;
        while (!(((_cursor474)._parent9) == null)) {
            _cursor474 = (_cursor474)._parent9;
            (_cursor474)._height10 = 1 + ((((((_cursor474)._left7) == null) ? (-1) : (((_cursor474)._left7)._height10)) > ((((_cursor474)._right8) == null) ? (-1) : (((_cursor474)._right8)._height10))) ? ((((_cursor474)._left7) == null) ? (-1) : (((_cursor474)._left7)._height10)) : ((((_cursor474)._right8) == null) ? (-1) : (((_cursor474)._right8)._height10)));
            _imbalance475 = ((((_cursor474)._left7) == null) ? (-1) : (((_cursor474)._left7)._height10)) - ((((_cursor474)._right8) == null) ? (-1) : (((_cursor474)._right8)._height10));
            if ((_imbalance475) > (1)) {
                if ((((((_cursor474)._left7)._left7) == null) ? (-1) : ((((_cursor474)._left7)._left7)._height10)) < (((((_cursor474)._left7)._right8) == null) ? (-1) : ((((_cursor474)._left7)._right8)._height10))) {
                    /* rotate ((_cursor474)._left7)._right8 */
                    var _a476 = (_cursor474)._left7;
                    var _b477 = (_a476)._right8;
                    var _c478 = (_b477)._left7;
                    /* replace _a476 with _b477 in (_a476)._parent9 */
                    if (!(((_a476)._parent9) == null)) {
                        if ((((_a476)._parent9)._left7) == (_a476)) {
                            ((_a476)._parent9)._left7 = _b477;
                        } else {
                            ((_a476)._parent9)._right8 = _b477;
                        }
                    }
                    if (!((_b477) == null)) {
                        (_b477)._parent9 = (_a476)._parent9;
                    }
                    /* replace _c478 with _a476 in _b477 */
                    (_b477)._left7 = _a476;
                    if (!((_a476) == null)) {
                        (_a476)._parent9 = _b477;
                    }
                    /* replace _b477 with _c478 in _a476 */
                    (_a476)._right8 = _c478;
                    if (!((_c478) == null)) {
                        (_c478)._parent9 = _a476;
                    }
                    /* _min_ax12 is min of ax1 */
                    var _augval479 = (_a476).ax1;
                    var _child480 = (_a476)._left7;
                    if (!((_child480) == null)) {
                        var _val481 = (_child480)._min_ax12;
                        _augval479 = ((_augval479) < (_val481)) ? (_augval479) : (_val481);
                    }
                    var _child482 = (_a476)._right8;
                    if (!((_child482) == null)) {
                        var _val483 = (_child482)._min_ax12;
                        _augval479 = ((_augval479) < (_val483)) ? (_augval479) : (_val483);
                    }
                    (_a476)._min_ax12 = _augval479;
                    /* _min_ay13 is min of ay1 */
                    var _augval484 = (_a476).ay1;
                    var _child485 = (_a476)._left7;
                    if (!((_child485) == null)) {
                        var _val486 = (_child485)._min_ay13;
                        _augval484 = ((_augval484) < (_val486)) ? (_augval484) : (_val486);
                    }
                    var _child487 = (_a476)._right8;
                    if (!((_child487) == null)) {
                        var _val488 = (_child487)._min_ay13;
                        _augval484 = ((_augval484) < (_val488)) ? (_augval484) : (_val488);
                    }
                    (_a476)._min_ay13 = _augval484;
                    /* _max_ay24 is max of ay2 */
                    var _augval489 = (_a476).ay2;
                    var _child490 = (_a476)._left7;
                    if (!((_child490) == null)) {
                        var _val491 = (_child490)._max_ay24;
                        _augval489 = ((_augval489) < (_val491)) ? (_val491) : (_augval489);
                    }
                    var _child492 = (_a476)._right8;
                    if (!((_child492) == null)) {
                        var _val493 = (_child492)._max_ay24;
                        _augval489 = ((_augval489) < (_val493)) ? (_val493) : (_augval489);
                    }
                    (_a476)._max_ay24 = _augval489;
                    (_a476)._height10 = 1 + ((((((_a476)._left7) == null) ? (-1) : (((_a476)._left7)._height10)) > ((((_a476)._right8) == null) ? (-1) : (((_a476)._right8)._height10))) ? ((((_a476)._left7) == null) ? (-1) : (((_a476)._left7)._height10)) : ((((_a476)._right8) == null) ? (-1) : (((_a476)._right8)._height10)));
                    /* _min_ax12 is min of ax1 */
                    var _augval494 = (_b477).ax1;
                    var _child495 = (_b477)._left7;
                    if (!((_child495) == null)) {
                        var _val496 = (_child495)._min_ax12;
                        _augval494 = ((_augval494) < (_val496)) ? (_augval494) : (_val496);
                    }
                    var _child497 = (_b477)._right8;
                    if (!((_child497) == null)) {
                        var _val498 = (_child497)._min_ax12;
                        _augval494 = ((_augval494) < (_val498)) ? (_augval494) : (_val498);
                    }
                    (_b477)._min_ax12 = _augval494;
                    /* _min_ay13 is min of ay1 */
                    var _augval499 = (_b477).ay1;
                    var _child500 = (_b477)._left7;
                    if (!((_child500) == null)) {
                        var _val501 = (_child500)._min_ay13;
                        _augval499 = ((_augval499) < (_val501)) ? (_augval499) : (_val501);
                    }
                    var _child502 = (_b477)._right8;
                    if (!((_child502) == null)) {
                        var _val503 = (_child502)._min_ay13;
                        _augval499 = ((_augval499) < (_val503)) ? (_augval499) : (_val503);
                    }
                    (_b477)._min_ay13 = _augval499;
                    /* _max_ay24 is max of ay2 */
                    var _augval504 = (_b477).ay2;
                    var _child505 = (_b477)._left7;
                    if (!((_child505) == null)) {
                        var _val506 = (_child505)._max_ay24;
                        _augval504 = ((_augval504) < (_val506)) ? (_val506) : (_augval504);
                    }
                    var _child507 = (_b477)._right8;
                    if (!((_child507) == null)) {
                        var _val508 = (_child507)._max_ay24;
                        _augval504 = ((_augval504) < (_val508)) ? (_val508) : (_augval504);
                    }
                    (_b477)._max_ay24 = _augval504;
                    (_b477)._height10 = 1 + ((((((_b477)._left7) == null) ? (-1) : (((_b477)._left7)._height10)) > ((((_b477)._right8) == null) ? (-1) : (((_b477)._right8)._height10))) ? ((((_b477)._left7) == null) ? (-1) : (((_b477)._left7)._height10)) : ((((_b477)._right8) == null) ? (-1) : (((_b477)._right8)._height10)));
                    if (!(((_b477)._parent9) == null)) {
                        /* _min_ax12 is min of ax1 */
                        var _augval509 = ((_b477)._parent9).ax1;
                        var _child510 = ((_b477)._parent9)._left7;
                        if (!((_child510) == null)) {
                            var _val511 = (_child510)._min_ax12;
                            _augval509 = ((_augval509) < (_val511)) ? (_augval509) : (_val511);
                        }
                        var _child512 = ((_b477)._parent9)._right8;
                        if (!((_child512) == null)) {
                            var _val513 = (_child512)._min_ax12;
                            _augval509 = ((_augval509) < (_val513)) ? (_augval509) : (_val513);
                        }
                        ((_b477)._parent9)._min_ax12 = _augval509;
                        /* _min_ay13 is min of ay1 */
                        var _augval514 = ((_b477)._parent9).ay1;
                        var _child515 = ((_b477)._parent9)._left7;
                        if (!((_child515) == null)) {
                            var _val516 = (_child515)._min_ay13;
                            _augval514 = ((_augval514) < (_val516)) ? (_augval514) : (_val516);
                        }
                        var _child517 = ((_b477)._parent9)._right8;
                        if (!((_child517) == null)) {
                            var _val518 = (_child517)._min_ay13;
                            _augval514 = ((_augval514) < (_val518)) ? (_augval514) : (_val518);
                        }
                        ((_b477)._parent9)._min_ay13 = _augval514;
                        /* _max_ay24 is max of ay2 */
                        var _augval519 = ((_b477)._parent9).ay2;
                        var _child520 = ((_b477)._parent9)._left7;
                        if (!((_child520) == null)) {
                            var _val521 = (_child520)._max_ay24;
                            _augval519 = ((_augval519) < (_val521)) ? (_val521) : (_augval519);
                        }
                        var _child522 = ((_b477)._parent9)._right8;
                        if (!((_child522) == null)) {
                            var _val523 = (_child522)._max_ay24;
                            _augval519 = ((_augval519) < (_val523)) ? (_val523) : (_augval519);
                        }
                        ((_b477)._parent9)._max_ay24 = _augval519;
                        ((_b477)._parent9)._height10 = 1 + (((((((_b477)._parent9)._left7) == null) ? (-1) : ((((_b477)._parent9)._left7)._height10)) > (((((_b477)._parent9)._right8) == null) ? (-1) : ((((_b477)._parent9)._right8)._height10))) ? (((((_b477)._parent9)._left7) == null) ? (-1) : ((((_b477)._parent9)._left7)._height10)) : (((((_b477)._parent9)._right8) == null) ? (-1) : ((((_b477)._parent9)._right8)._height10)));
                    } else {
                        (this)._root1 = _b477;
                    }
                }
                /* rotate (_cursor474)._left7 */
                var _a524 = _cursor474;
                var _b525 = (_a524)._left7;
                var _c526 = (_b525)._right8;
                /* replace _a524 with _b525 in (_a524)._parent9 */
                if (!(((_a524)._parent9) == null)) {
                    if ((((_a524)._parent9)._left7) == (_a524)) {
                        ((_a524)._parent9)._left7 = _b525;
                    } else {
                        ((_a524)._parent9)._right8 = _b525;
                    }
                }
                if (!((_b525) == null)) {
                    (_b525)._parent9 = (_a524)._parent9;
                }
                /* replace _c526 with _a524 in _b525 */
                (_b525)._right8 = _a524;
                if (!((_a524) == null)) {
                    (_a524)._parent9 = _b525;
                }
                /* replace _b525 with _c526 in _a524 */
                (_a524)._left7 = _c526;
                if (!((_c526) == null)) {
                    (_c526)._parent9 = _a524;
                }
                /* _min_ax12 is min of ax1 */
                var _augval527 = (_a524).ax1;
                var _child528 = (_a524)._left7;
                if (!((_child528) == null)) {
                    var _val529 = (_child528)._min_ax12;
                    _augval527 = ((_augval527) < (_val529)) ? (_augval527) : (_val529);
                }
                var _child530 = (_a524)._right8;
                if (!((_child530) == null)) {
                    var _val531 = (_child530)._min_ax12;
                    _augval527 = ((_augval527) < (_val531)) ? (_augval527) : (_val531);
                }
                (_a524)._min_ax12 = _augval527;
                /* _min_ay13 is min of ay1 */
                var _augval532 = (_a524).ay1;
                var _child533 = (_a524)._left7;
                if (!((_child533) == null)) {
                    var _val534 = (_child533)._min_ay13;
                    _augval532 = ((_augval532) < (_val534)) ? (_augval532) : (_val534);
                }
                var _child535 = (_a524)._right8;
                if (!((_child535) == null)) {
                    var _val536 = (_child535)._min_ay13;
                    _augval532 = ((_augval532) < (_val536)) ? (_augval532) : (_val536);
                }
                (_a524)._min_ay13 = _augval532;
                /* _max_ay24 is max of ay2 */
                var _augval537 = (_a524).ay2;
                var _child538 = (_a524)._left7;
                if (!((_child538) == null)) {
                    var _val539 = (_child538)._max_ay24;
                    _augval537 = ((_augval537) < (_val539)) ? (_val539) : (_augval537);
                }
                var _child540 = (_a524)._right8;
                if (!((_child540) == null)) {
                    var _val541 = (_child540)._max_ay24;
                    _augval537 = ((_augval537) < (_val541)) ? (_val541) : (_augval537);
                }
                (_a524)._max_ay24 = _augval537;
                (_a524)._height10 = 1 + ((((((_a524)._left7) == null) ? (-1) : (((_a524)._left7)._height10)) > ((((_a524)._right8) == null) ? (-1) : (((_a524)._right8)._height10))) ? ((((_a524)._left7) == null) ? (-1) : (((_a524)._left7)._height10)) : ((((_a524)._right8) == null) ? (-1) : (((_a524)._right8)._height10)));
                /* _min_ax12 is min of ax1 */
                var _augval542 = (_b525).ax1;
                var _child543 = (_b525)._left7;
                if (!((_child543) == null)) {
                    var _val544 = (_child543)._min_ax12;
                    _augval542 = ((_augval542) < (_val544)) ? (_augval542) : (_val544);
                }
                var _child545 = (_b525)._right8;
                if (!((_child545) == null)) {
                    var _val546 = (_child545)._min_ax12;
                    _augval542 = ((_augval542) < (_val546)) ? (_augval542) : (_val546);
                }
                (_b525)._min_ax12 = _augval542;
                /* _min_ay13 is min of ay1 */
                var _augval547 = (_b525).ay1;
                var _child548 = (_b525)._left7;
                if (!((_child548) == null)) {
                    var _val549 = (_child548)._min_ay13;
                    _augval547 = ((_augval547) < (_val549)) ? (_augval547) : (_val549);
                }
                var _child550 = (_b525)._right8;
                if (!((_child550) == null)) {
                    var _val551 = (_child550)._min_ay13;
                    _augval547 = ((_augval547) < (_val551)) ? (_augval547) : (_val551);
                }
                (_b525)._min_ay13 = _augval547;
                /* _max_ay24 is max of ay2 */
                var _augval552 = (_b525).ay2;
                var _child553 = (_b525)._left7;
                if (!((_child553) == null)) {
                    var _val554 = (_child553)._max_ay24;
                    _augval552 = ((_augval552) < (_val554)) ? (_val554) : (_augval552);
                }
                var _child555 = (_b525)._right8;
                if (!((_child555) == null)) {
                    var _val556 = (_child555)._max_ay24;
                    _augval552 = ((_augval552) < (_val556)) ? (_val556) : (_augval552);
                }
                (_b525)._max_ay24 = _augval552;
                (_b525)._height10 = 1 + ((((((_b525)._left7) == null) ? (-1) : (((_b525)._left7)._height10)) > ((((_b525)._right8) == null) ? (-1) : (((_b525)._right8)._height10))) ? ((((_b525)._left7) == null) ? (-1) : (((_b525)._left7)._height10)) : ((((_b525)._right8) == null) ? (-1) : (((_b525)._right8)._height10)));
                if (!(((_b525)._parent9) == null)) {
                    /* _min_ax12 is min of ax1 */
                    var _augval557 = ((_b525)._parent9).ax1;
                    var _child558 = ((_b525)._parent9)._left7;
                    if (!((_child558) == null)) {
                        var _val559 = (_child558)._min_ax12;
                        _augval557 = ((_augval557) < (_val559)) ? (_augval557) : (_val559);
                    }
                    var _child560 = ((_b525)._parent9)._right8;
                    if (!((_child560) == null)) {
                        var _val561 = (_child560)._min_ax12;
                        _augval557 = ((_augval557) < (_val561)) ? (_augval557) : (_val561);
                    }
                    ((_b525)._parent9)._min_ax12 = _augval557;
                    /* _min_ay13 is min of ay1 */
                    var _augval562 = ((_b525)._parent9).ay1;
                    var _child563 = ((_b525)._parent9)._left7;
                    if (!((_child563) == null)) {
                        var _val564 = (_child563)._min_ay13;
                        _augval562 = ((_augval562) < (_val564)) ? (_augval562) : (_val564);
                    }
                    var _child565 = ((_b525)._parent9)._right8;
                    if (!((_child565) == null)) {
                        var _val566 = (_child565)._min_ay13;
                        _augval562 = ((_augval562) < (_val566)) ? (_augval562) : (_val566);
                    }
                    ((_b525)._parent9)._min_ay13 = _augval562;
                    /* _max_ay24 is max of ay2 */
                    var _augval567 = ((_b525)._parent9).ay2;
                    var _child568 = ((_b525)._parent9)._left7;
                    if (!((_child568) == null)) {
                        var _val569 = (_child568)._max_ay24;
                        _augval567 = ((_augval567) < (_val569)) ? (_val569) : (_augval567);
                    }
                    var _child570 = ((_b525)._parent9)._right8;
                    if (!((_child570) == null)) {
                        var _val571 = (_child570)._max_ay24;
                        _augval567 = ((_augval567) < (_val571)) ? (_val571) : (_augval567);
                    }
                    ((_b525)._parent9)._max_ay24 = _augval567;
                    ((_b525)._parent9)._height10 = 1 + (((((((_b525)._parent9)._left7) == null) ? (-1) : ((((_b525)._parent9)._left7)._height10)) > (((((_b525)._parent9)._right8) == null) ? (-1) : ((((_b525)._parent9)._right8)._height10))) ? (((((_b525)._parent9)._left7) == null) ? (-1) : ((((_b525)._parent9)._left7)._height10)) : (((((_b525)._parent9)._right8) == null) ? (-1) : ((((_b525)._parent9)._right8)._height10)));
                } else {
                    (this)._root1 = _b525;
                }
                _cursor474 = (_cursor474)._parent9;
            } else if ((_imbalance475) < (-1)) {
                if ((((((_cursor474)._right8)._left7) == null) ? (-1) : ((((_cursor474)._right8)._left7)._height10)) > (((((_cursor474)._right8)._right8) == null) ? (-1) : ((((_cursor474)._right8)._right8)._height10))) {
                    /* rotate ((_cursor474)._right8)._left7 */
                    var _a572 = (_cursor474)._right8;
                    var _b573 = (_a572)._left7;
                    var _c574 = (_b573)._right8;
                    /* replace _a572 with _b573 in (_a572)._parent9 */
                    if (!(((_a572)._parent9) == null)) {
                        if ((((_a572)._parent9)._left7) == (_a572)) {
                            ((_a572)._parent9)._left7 = _b573;
                        } else {
                            ((_a572)._parent9)._right8 = _b573;
                        }
                    }
                    if (!((_b573) == null)) {
                        (_b573)._parent9 = (_a572)._parent9;
                    }
                    /* replace _c574 with _a572 in _b573 */
                    (_b573)._right8 = _a572;
                    if (!((_a572) == null)) {
                        (_a572)._parent9 = _b573;
                    }
                    /* replace _b573 with _c574 in _a572 */
                    (_a572)._left7 = _c574;
                    if (!((_c574) == null)) {
                        (_c574)._parent9 = _a572;
                    }
                    /* _min_ax12 is min of ax1 */
                    var _augval575 = (_a572).ax1;
                    var _child576 = (_a572)._left7;
                    if (!((_child576) == null)) {
                        var _val577 = (_child576)._min_ax12;
                        _augval575 = ((_augval575) < (_val577)) ? (_augval575) : (_val577);
                    }
                    var _child578 = (_a572)._right8;
                    if (!((_child578) == null)) {
                        var _val579 = (_child578)._min_ax12;
                        _augval575 = ((_augval575) < (_val579)) ? (_augval575) : (_val579);
                    }
                    (_a572)._min_ax12 = _augval575;
                    /* _min_ay13 is min of ay1 */
                    var _augval580 = (_a572).ay1;
                    var _child581 = (_a572)._left7;
                    if (!((_child581) == null)) {
                        var _val582 = (_child581)._min_ay13;
                        _augval580 = ((_augval580) < (_val582)) ? (_augval580) : (_val582);
                    }
                    var _child583 = (_a572)._right8;
                    if (!((_child583) == null)) {
                        var _val584 = (_child583)._min_ay13;
                        _augval580 = ((_augval580) < (_val584)) ? (_augval580) : (_val584);
                    }
                    (_a572)._min_ay13 = _augval580;
                    /* _max_ay24 is max of ay2 */
                    var _augval585 = (_a572).ay2;
                    var _child586 = (_a572)._left7;
                    if (!((_child586) == null)) {
                        var _val587 = (_child586)._max_ay24;
                        _augval585 = ((_augval585) < (_val587)) ? (_val587) : (_augval585);
                    }
                    var _child588 = (_a572)._right8;
                    if (!((_child588) == null)) {
                        var _val589 = (_child588)._max_ay24;
                        _augval585 = ((_augval585) < (_val589)) ? (_val589) : (_augval585);
                    }
                    (_a572)._max_ay24 = _augval585;
                    (_a572)._height10 = 1 + ((((((_a572)._left7) == null) ? (-1) : (((_a572)._left7)._height10)) > ((((_a572)._right8) == null) ? (-1) : (((_a572)._right8)._height10))) ? ((((_a572)._left7) == null) ? (-1) : (((_a572)._left7)._height10)) : ((((_a572)._right8) == null) ? (-1) : (((_a572)._right8)._height10)));
                    /* _min_ax12 is min of ax1 */
                    var _augval590 = (_b573).ax1;
                    var _child591 = (_b573)._left7;
                    if (!((_child591) == null)) {
                        var _val592 = (_child591)._min_ax12;
                        _augval590 = ((_augval590) < (_val592)) ? (_augval590) : (_val592);
                    }
                    var _child593 = (_b573)._right8;
                    if (!((_child593) == null)) {
                        var _val594 = (_child593)._min_ax12;
                        _augval590 = ((_augval590) < (_val594)) ? (_augval590) : (_val594);
                    }
                    (_b573)._min_ax12 = _augval590;
                    /* _min_ay13 is min of ay1 */
                    var _augval595 = (_b573).ay1;
                    var _child596 = (_b573)._left7;
                    if (!((_child596) == null)) {
                        var _val597 = (_child596)._min_ay13;
                        _augval595 = ((_augval595) < (_val597)) ? (_augval595) : (_val597);
                    }
                    var _child598 = (_b573)._right8;
                    if (!((_child598) == null)) {
                        var _val599 = (_child598)._min_ay13;
                        _augval595 = ((_augval595) < (_val599)) ? (_augval595) : (_val599);
                    }
                    (_b573)._min_ay13 = _augval595;
                    /* _max_ay24 is max of ay2 */
                    var _augval600 = (_b573).ay2;
                    var _child601 = (_b573)._left7;
                    if (!((_child601) == null)) {
                        var _val602 = (_child601)._max_ay24;
                        _augval600 = ((_augval600) < (_val602)) ? (_val602) : (_augval600);
                    }
                    var _child603 = (_b573)._right8;
                    if (!((_child603) == null)) {
                        var _val604 = (_child603)._max_ay24;
                        _augval600 = ((_augval600) < (_val604)) ? (_val604) : (_augval600);
                    }
                    (_b573)._max_ay24 = _augval600;
                    (_b573)._height10 = 1 + ((((((_b573)._left7) == null) ? (-1) : (((_b573)._left7)._height10)) > ((((_b573)._right8) == null) ? (-1) : (((_b573)._right8)._height10))) ? ((((_b573)._left7) == null) ? (-1) : (((_b573)._left7)._height10)) : ((((_b573)._right8) == null) ? (-1) : (((_b573)._right8)._height10)));
                    if (!(((_b573)._parent9) == null)) {
                        /* _min_ax12 is min of ax1 */
                        var _augval605 = ((_b573)._parent9).ax1;
                        var _child606 = ((_b573)._parent9)._left7;
                        if (!((_child606) == null)) {
                            var _val607 = (_child606)._min_ax12;
                            _augval605 = ((_augval605) < (_val607)) ? (_augval605) : (_val607);
                        }
                        var _child608 = ((_b573)._parent9)._right8;
                        if (!((_child608) == null)) {
                            var _val609 = (_child608)._min_ax12;
                            _augval605 = ((_augval605) < (_val609)) ? (_augval605) : (_val609);
                        }
                        ((_b573)._parent9)._min_ax12 = _augval605;
                        /* _min_ay13 is min of ay1 */
                        var _augval610 = ((_b573)._parent9).ay1;
                        var _child611 = ((_b573)._parent9)._left7;
                        if (!((_child611) == null)) {
                            var _val612 = (_child611)._min_ay13;
                            _augval610 = ((_augval610) < (_val612)) ? (_augval610) : (_val612);
                        }
                        var _child613 = ((_b573)._parent9)._right8;
                        if (!((_child613) == null)) {
                            var _val614 = (_child613)._min_ay13;
                            _augval610 = ((_augval610) < (_val614)) ? (_augval610) : (_val614);
                        }
                        ((_b573)._parent9)._min_ay13 = _augval610;
                        /* _max_ay24 is max of ay2 */
                        var _augval615 = ((_b573)._parent9).ay2;
                        var _child616 = ((_b573)._parent9)._left7;
                        if (!((_child616) == null)) {
                            var _val617 = (_child616)._max_ay24;
                            _augval615 = ((_augval615) < (_val617)) ? (_val617) : (_augval615);
                        }
                        var _child618 = ((_b573)._parent9)._right8;
                        if (!((_child618) == null)) {
                            var _val619 = (_child618)._max_ay24;
                            _augval615 = ((_augval615) < (_val619)) ? (_val619) : (_augval615);
                        }
                        ((_b573)._parent9)._max_ay24 = _augval615;
                        ((_b573)._parent9)._height10 = 1 + (((((((_b573)._parent9)._left7) == null) ? (-1) : ((((_b573)._parent9)._left7)._height10)) > (((((_b573)._parent9)._right8) == null) ? (-1) : ((((_b573)._parent9)._right8)._height10))) ? (((((_b573)._parent9)._left7) == null) ? (-1) : ((((_b573)._parent9)._left7)._height10)) : (((((_b573)._parent9)._right8) == null) ? (-1) : ((((_b573)._parent9)._right8)._height10)));
                    } else {
                        (this)._root1 = _b573;
                    }
                }
                /* rotate (_cursor474)._right8 */
                var _a620 = _cursor474;
                var _b621 = (_a620)._right8;
                var _c622 = (_b621)._left7;
                /* replace _a620 with _b621 in (_a620)._parent9 */
                if (!(((_a620)._parent9) == null)) {
                    if ((((_a620)._parent9)._left7) == (_a620)) {
                        ((_a620)._parent9)._left7 = _b621;
                    } else {
                        ((_a620)._parent9)._right8 = _b621;
                    }
                }
                if (!((_b621) == null)) {
                    (_b621)._parent9 = (_a620)._parent9;
                }
                /* replace _c622 with _a620 in _b621 */
                (_b621)._left7 = _a620;
                if (!((_a620) == null)) {
                    (_a620)._parent9 = _b621;
                }
                /* replace _b621 with _c622 in _a620 */
                (_a620)._right8 = _c622;
                if (!((_c622) == null)) {
                    (_c622)._parent9 = _a620;
                }
                /* _min_ax12 is min of ax1 */
                var _augval623 = (_a620).ax1;
                var _child624 = (_a620)._left7;
                if (!((_child624) == null)) {
                    var _val625 = (_child624)._min_ax12;
                    _augval623 = ((_augval623) < (_val625)) ? (_augval623) : (_val625);
                }
                var _child626 = (_a620)._right8;
                if (!((_child626) == null)) {
                    var _val627 = (_child626)._min_ax12;
                    _augval623 = ((_augval623) < (_val627)) ? (_augval623) : (_val627);
                }
                (_a620)._min_ax12 = _augval623;
                /* _min_ay13 is min of ay1 */
                var _augval628 = (_a620).ay1;
                var _child629 = (_a620)._left7;
                if (!((_child629) == null)) {
                    var _val630 = (_child629)._min_ay13;
                    _augval628 = ((_augval628) < (_val630)) ? (_augval628) : (_val630);
                }
                var _child631 = (_a620)._right8;
                if (!((_child631) == null)) {
                    var _val632 = (_child631)._min_ay13;
                    _augval628 = ((_augval628) < (_val632)) ? (_augval628) : (_val632);
                }
                (_a620)._min_ay13 = _augval628;
                /* _max_ay24 is max of ay2 */
                var _augval633 = (_a620).ay2;
                var _child634 = (_a620)._left7;
                if (!((_child634) == null)) {
                    var _val635 = (_child634)._max_ay24;
                    _augval633 = ((_augval633) < (_val635)) ? (_val635) : (_augval633);
                }
                var _child636 = (_a620)._right8;
                if (!((_child636) == null)) {
                    var _val637 = (_child636)._max_ay24;
                    _augval633 = ((_augval633) < (_val637)) ? (_val637) : (_augval633);
                }
                (_a620)._max_ay24 = _augval633;
                (_a620)._height10 = 1 + ((((((_a620)._left7) == null) ? (-1) : (((_a620)._left7)._height10)) > ((((_a620)._right8) == null) ? (-1) : (((_a620)._right8)._height10))) ? ((((_a620)._left7) == null) ? (-1) : (((_a620)._left7)._height10)) : ((((_a620)._right8) == null) ? (-1) : (((_a620)._right8)._height10)));
                /* _min_ax12 is min of ax1 */
                var _augval638 = (_b621).ax1;
                var _child639 = (_b621)._left7;
                if (!((_child639) == null)) {
                    var _val640 = (_child639)._min_ax12;
                    _augval638 = ((_augval638) < (_val640)) ? (_augval638) : (_val640);
                }
                var _child641 = (_b621)._right8;
                if (!((_child641) == null)) {
                    var _val642 = (_child641)._min_ax12;
                    _augval638 = ((_augval638) < (_val642)) ? (_augval638) : (_val642);
                }
                (_b621)._min_ax12 = _augval638;
                /* _min_ay13 is min of ay1 */
                var _augval643 = (_b621).ay1;
                var _child644 = (_b621)._left7;
                if (!((_child644) == null)) {
                    var _val645 = (_child644)._min_ay13;
                    _augval643 = ((_augval643) < (_val645)) ? (_augval643) : (_val645);
                }
                var _child646 = (_b621)._right8;
                if (!((_child646) == null)) {
                    var _val647 = (_child646)._min_ay13;
                    _augval643 = ((_augval643) < (_val647)) ? (_augval643) : (_val647);
                }
                (_b621)._min_ay13 = _augval643;
                /* _max_ay24 is max of ay2 */
                var _augval648 = (_b621).ay2;
                var _child649 = (_b621)._left7;
                if (!((_child649) == null)) {
                    var _val650 = (_child649)._max_ay24;
                    _augval648 = ((_augval648) < (_val650)) ? (_val650) : (_augval648);
                }
                var _child651 = (_b621)._right8;
                if (!((_child651) == null)) {
                    var _val652 = (_child651)._max_ay24;
                    _augval648 = ((_augval648) < (_val652)) ? (_val652) : (_augval648);
                }
                (_b621)._max_ay24 = _augval648;
                (_b621)._height10 = 1 + ((((((_b621)._left7) == null) ? (-1) : (((_b621)._left7)._height10)) > ((((_b621)._right8) == null) ? (-1) : (((_b621)._right8)._height10))) ? ((((_b621)._left7) == null) ? (-1) : (((_b621)._left7)._height10)) : ((((_b621)._right8) == null) ? (-1) : (((_b621)._right8)._height10)));
                if (!(((_b621)._parent9) == null)) {
                    /* _min_ax12 is min of ax1 */
                    var _augval653 = ((_b621)._parent9).ax1;
                    var _child654 = ((_b621)._parent9)._left7;
                    if (!((_child654) == null)) {
                        var _val655 = (_child654)._min_ax12;
                        _augval653 = ((_augval653) < (_val655)) ? (_augval653) : (_val655);
                    }
                    var _child656 = ((_b621)._parent9)._right8;
                    if (!((_child656) == null)) {
                        var _val657 = (_child656)._min_ax12;
                        _augval653 = ((_augval653) < (_val657)) ? (_augval653) : (_val657);
                    }
                    ((_b621)._parent9)._min_ax12 = _augval653;
                    /* _min_ay13 is min of ay1 */
                    var _augval658 = ((_b621)._parent9).ay1;
                    var _child659 = ((_b621)._parent9)._left7;
                    if (!((_child659) == null)) {
                        var _val660 = (_child659)._min_ay13;
                        _augval658 = ((_augval658) < (_val660)) ? (_augval658) : (_val660);
                    }
                    var _child661 = ((_b621)._parent9)._right8;
                    if (!((_child661) == null)) {
                        var _val662 = (_child661)._min_ay13;
                        _augval658 = ((_augval658) < (_val662)) ? (_augval658) : (_val662);
                    }
                    ((_b621)._parent9)._min_ay13 = _augval658;
                    /* _max_ay24 is max of ay2 */
                    var _augval663 = ((_b621)._parent9).ay2;
                    var _child664 = ((_b621)._parent9)._left7;
                    if (!((_child664) == null)) {
                        var _val665 = (_child664)._max_ay24;
                        _augval663 = ((_augval663) < (_val665)) ? (_val665) : (_augval663);
                    }
                    var _child666 = ((_b621)._parent9)._right8;
                    if (!((_child666) == null)) {
                        var _val667 = (_child666)._max_ay24;
                        _augval663 = ((_augval663) < (_val667)) ? (_val667) : (_augval663);
                    }
                    ((_b621)._parent9)._max_ay24 = _augval663;
                    ((_b621)._parent9)._height10 = 1 + (((((((_b621)._parent9)._left7) == null) ? (-1) : ((((_b621)._parent9)._left7)._height10)) > (((((_b621)._parent9)._right8) == null) ? (-1) : ((((_b621)._parent9)._right8)._height10))) ? (((((_b621)._parent9)._left7) == null) ? (-1) : ((((_b621)._parent9)._left7)._height10)) : (((((_b621)._parent9)._right8) == null) ? (-1) : ((((_b621)._parent9)._right8)._height10)));
                } else {
                    (this)._root1 = _b621;
                }
                _cursor474 = (_cursor474)._parent9;
            }
        }
        (__x).ax2 = new_val;
    }
}
RectangleHolder.prototype.updateAy2 = function (__x, new_val) {
    if ((__x).ay2 != new_val) {
        /* _max_ay24 is max of ay2 */
        var _augval668 = new_val;
        var _child669 = (__x)._left7;
        if (!((_child669) == null)) {
            var _val670 = (_child669)._max_ay24;
            _augval668 = ((_augval668) < (_val670)) ? (_val670) : (_augval668);
        }
        var _child671 = (__x)._right8;
        if (!((_child671) == null)) {
            var _val672 = (_child671)._max_ay24;
            _augval668 = ((_augval668) < (_val672)) ? (_val672) : (_augval668);
        }
        (__x)._max_ay24 = _augval668;
        var _cursor673 = (__x)._parent9;
        var _changed674 = true;
        while ((_changed674) && (!((_cursor673) == (null)))) {
            var _old__max_ay24675 = (_cursor673)._max_ay24;
            var _old_height676 = (_cursor673)._height10;
            /* _max_ay24 is max of ay2 */
            var _augval677 = (_cursor673).ay2;
            var _child678 = (_cursor673)._left7;
            if (!((_child678) == null)) {
                var _val679 = (_child678)._max_ay24;
                _augval677 = ((_augval677) < (_val679)) ? (_val679) : (_augval677);
            }
            var _child680 = (_cursor673)._right8;
            if (!((_child680) == null)) {
                var _val681 = (_child680)._max_ay24;
                _augval677 = ((_augval677) < (_val681)) ? (_val681) : (_augval677);
            }
            (_cursor673)._max_ay24 = _augval677;
            (_cursor673)._height10 = 1 + ((((((_cursor673)._left7) == null) ? (-1) : (((_cursor673)._left7)._height10)) > ((((_cursor673)._right8) == null) ? (-1) : (((_cursor673)._right8)._height10))) ? ((((_cursor673)._left7) == null) ? (-1) : (((_cursor673)._left7)._height10)) : ((((_cursor673)._right8) == null) ? (-1) : (((_cursor673)._right8)._height10)));
            _changed674 = false;
            _changed674 = (_changed674) || (!((_old__max_ay24675) == ((_cursor673)._max_ay24)));
            _changed674 = (_changed674) || (!((_old_height676) == ((_cursor673)._height10)));
            _cursor673 = (_cursor673)._parent9;
        }
        (__x).ay2 = new_val;
    }
}
RectangleHolder.prototype.update = function (__x, ax1, ay1, ax2, ay2) {
    var _parent682 = (__x)._parent9;
    var _left683 = (__x)._left7;
    var _right684 = (__x)._right8;
    var _new_x685;
    if (((_left683) == null) && ((_right684) == null)) {
        _new_x685 = null;
        /* replace __x with _new_x685 in _parent682 */
        if (!((_parent682) == null)) {
            if (((_parent682)._left7) == (__x)) {
                (_parent682)._left7 = _new_x685;
            } else {
                (_parent682)._right8 = _new_x685;
            }
        }
        if (!((_new_x685) == null)) {
            (_new_x685)._parent9 = _parent682;
        }
    } else if ((!((_left683) == null)) && ((_right684) == null)) {
        _new_x685 = _left683;
        /* replace __x with _new_x685 in _parent682 */
        if (!((_parent682) == null)) {
            if (((_parent682)._left7) == (__x)) {
                (_parent682)._left7 = _new_x685;
            } else {
                (_parent682)._right8 = _new_x685;
            }
        }
        if (!((_new_x685) == null)) {
            (_new_x685)._parent9 = _parent682;
        }
    } else if (((_left683) == null) && (!((_right684) == null))) {
        _new_x685 = _right684;
        /* replace __x with _new_x685 in _parent682 */
        if (!((_parent682) == null)) {
            if (((_parent682)._left7) == (__x)) {
                (_parent682)._left7 = _new_x685;
            } else {
                (_parent682)._right8 = _new_x685;
            }
        }
        if (!((_new_x685) == null)) {
            (_new_x685)._parent9 = _parent682;
        }
    } else {
        var _root686 = (__x)._right8;
        var _x687 = _root686;
        var _descend688 = true;
        var _from_left689 = true;
        while (true) {
            if ((_x687) == null) {
                _x687 = null;
                break;
            }
            if (_descend688) {
                /* too small? */
                if (false) {
                    if ((!(((_x687)._right8) == null)) && (true)) {
                        if ((_x687) == (_root686)) {
                            _root686 = (_x687)._right8;
                        }
                        _x687 = (_x687)._right8;
                    } else if ((_x687) == (_root686)) {
                        _x687 = null;
                        break;
                    } else {
                        _descend688 = false;
                        _from_left689 = (!(((_x687)._parent9) == null)) && ((_x687) == (((_x687)._parent9)._left7));
                        _x687 = (_x687)._parent9;
                    }
                } else if ((!(((_x687)._left7) == null)) && (true)) {
                    _x687 = (_x687)._left7;
                    /* too large? */
                } else if (false) {
                    if ((_x687) == (_root686)) {
                        _x687 = null;
                        break;
                    } else {
                        _descend688 = false;
                        _from_left689 = (!(((_x687)._parent9) == null)) && ((_x687) == (((_x687)._parent9)._left7));
                        _x687 = (_x687)._parent9;
                    }
                    /* node ok? */
                } else if (true) {
                    break;
                } else if ((_x687) == (_root686)) {
                    _root686 = (_x687)._right8;
                    _x687 = (_x687)._right8;
                } else {
                    if ((!(((_x687)._right8) == null)) && (true)) {
                        if ((_x687) == (_root686)) {
                            _root686 = (_x687)._right8;
                        }
                        _x687 = (_x687)._right8;
                    } else {
                        _descend688 = false;
                        _from_left689 = (!(((_x687)._parent9) == null)) && ((_x687) == (((_x687)._parent9)._left7));
                        _x687 = (_x687)._parent9;
                    }
                }
            } else if (_from_left689) {
                if (false) {
                    _x687 = null;
                    break;
                } else if (true) {
                    break;
                } else if ((!(((_x687)._right8) == null)) && (true)) {
                    _descend688 = true;
                    if ((_x687) == (_root686)) {
                        _root686 = (_x687)._right8;
                    }
                    _x687 = (_x687)._right8;
                } else if ((_x687) == (_root686)) {
                    _x687 = null;
                    break;
                } else {
                    _descend688 = false;
                    _from_left689 = (!(((_x687)._parent9) == null)) && ((_x687) == (((_x687)._parent9)._left7));
                    _x687 = (_x687)._parent9;
                }
            } else {
                if ((_x687) == (_root686)) {
                    _x687 = null;
                    break;
                } else {
                    _descend688 = false;
                    _from_left689 = (!(((_x687)._parent9) == null)) && ((_x687) == (((_x687)._parent9)._left7));
                    _x687 = (_x687)._parent9;
                }
            }
        }
        _new_x685 = _x687;
        var _mp690 = (_x687)._parent9;
        var _mr691 = (_x687)._right8;
        /* replace _x687 with _mr691 in _mp690 */
        if (!((_mp690) == null)) {
            if (((_mp690)._left7) == (_x687)) {
                (_mp690)._left7 = _mr691;
            } else {
                (_mp690)._right8 = _mr691;
            }
        }
        if (!((_mr691) == null)) {
            (_mr691)._parent9 = _mp690;
        }
        /* replace __x with _x687 in _parent682 */
        if (!((_parent682) == null)) {
            if (((_parent682)._left7) == (__x)) {
                (_parent682)._left7 = _x687;
            } else {
                (_parent682)._right8 = _x687;
            }
        }
        if (!((_x687) == null)) {
            (_x687)._parent9 = _parent682;
        }
        /* replace null with _left683 in _x687 */
        (_x687)._left7 = _left683;
        if (!((_left683) == null)) {
            (_left683)._parent9 = _x687;
        }
        /* replace _mr691 with (__x)._right8 in _x687 */
        (_x687)._right8 = (__x)._right8;
        if (!(((__x)._right8) == null)) {
            ((__x)._right8)._parent9 = _x687;
        }
        /* _min_ax12 is min of ax1 */
        var _augval692 = (_x687).ax1;
        var _child693 = (_x687)._left7;
        if (!((_child693) == null)) {
            var _val694 = (_child693)._min_ax12;
            _augval692 = ((_augval692) < (_val694)) ? (_augval692) : (_val694);
        }
        var _child695 = (_x687)._right8;
        if (!((_child695) == null)) {
            var _val696 = (_child695)._min_ax12;
            _augval692 = ((_augval692) < (_val696)) ? (_augval692) : (_val696);
        }
        (_x687)._min_ax12 = _augval692;
        /* _min_ay13 is min of ay1 */
        var _augval697 = (_x687).ay1;
        var _child698 = (_x687)._left7;
        if (!((_child698) == null)) {
            var _val699 = (_child698)._min_ay13;
            _augval697 = ((_augval697) < (_val699)) ? (_augval697) : (_val699);
        }
        var _child700 = (_x687)._right8;
        if (!((_child700) == null)) {
            var _val701 = (_child700)._min_ay13;
            _augval697 = ((_augval697) < (_val701)) ? (_augval697) : (_val701);
        }
        (_x687)._min_ay13 = _augval697;
        /* _max_ay24 is max of ay2 */
        var _augval702 = (_x687).ay2;
        var _child703 = (_x687)._left7;
        if (!((_child703) == null)) {
            var _val704 = (_child703)._max_ay24;
            _augval702 = ((_augval702) < (_val704)) ? (_val704) : (_augval702);
        }
        var _child705 = (_x687)._right8;
        if (!((_child705) == null)) {
            var _val706 = (_child705)._max_ay24;
            _augval702 = ((_augval702) < (_val706)) ? (_val706) : (_augval702);
        }
        (_x687)._max_ay24 = _augval702;
        (_x687)._height10 = 1 + ((((((_x687)._left7) == null) ? (-1) : (((_x687)._left7)._height10)) > ((((_x687)._right8) == null) ? (-1) : (((_x687)._right8)._height10))) ? ((((_x687)._left7) == null) ? (-1) : (((_x687)._left7)._height10)) : ((((_x687)._right8) == null) ? (-1) : (((_x687)._right8)._height10)));
        var _cursor707 = _mp690;
        var _changed708 = true;
        while ((_changed708) && (!((_cursor707) == (_parent682)))) {
            var _old__min_ax12709 = (_cursor707)._min_ax12;
            var _old__min_ay13710 = (_cursor707)._min_ay13;
            var _old__max_ay24711 = (_cursor707)._max_ay24;
            var _old_height712 = (_cursor707)._height10;
            /* _min_ax12 is min of ax1 */
            var _augval713 = (_cursor707).ax1;
            var _child714 = (_cursor707)._left7;
            if (!((_child714) == null)) {
                var _val715 = (_child714)._min_ax12;
                _augval713 = ((_augval713) < (_val715)) ? (_augval713) : (_val715);
            }
            var _child716 = (_cursor707)._right8;
            if (!((_child716) == null)) {
                var _val717 = (_child716)._min_ax12;
                _augval713 = ((_augval713) < (_val717)) ? (_augval713) : (_val717);
            }
            (_cursor707)._min_ax12 = _augval713;
            /* _min_ay13 is min of ay1 */
            var _augval718 = (_cursor707).ay1;
            var _child719 = (_cursor707)._left7;
            if (!((_child719) == null)) {
                var _val720 = (_child719)._min_ay13;
                _augval718 = ((_augval718) < (_val720)) ? (_augval718) : (_val720);
            }
            var _child721 = (_cursor707)._right8;
            if (!((_child721) == null)) {
                var _val722 = (_child721)._min_ay13;
                _augval718 = ((_augval718) < (_val722)) ? (_augval718) : (_val722);
            }
            (_cursor707)._min_ay13 = _augval718;
            /* _max_ay24 is max of ay2 */
            var _augval723 = (_cursor707).ay2;
            var _child724 = (_cursor707)._left7;
            if (!((_child724) == null)) {
                var _val725 = (_child724)._max_ay24;
                _augval723 = ((_augval723) < (_val725)) ? (_val725) : (_augval723);
            }
            var _child726 = (_cursor707)._right8;
            if (!((_child726) == null)) {
                var _val727 = (_child726)._max_ay24;
                _augval723 = ((_augval723) < (_val727)) ? (_val727) : (_augval723);
            }
            (_cursor707)._max_ay24 = _augval723;
            (_cursor707)._height10 = 1 + ((((((_cursor707)._left7) == null) ? (-1) : (((_cursor707)._left7)._height10)) > ((((_cursor707)._right8) == null) ? (-1) : (((_cursor707)._right8)._height10))) ? ((((_cursor707)._left7) == null) ? (-1) : (((_cursor707)._left7)._height10)) : ((((_cursor707)._right8) == null) ? (-1) : (((_cursor707)._right8)._height10)));
            _changed708 = false;
            _changed708 = (_changed708) || (!((_old__min_ax12709) == ((_cursor707)._min_ax12)));
            _changed708 = (_changed708) || (!((_old__min_ay13710) == ((_cursor707)._min_ay13)));
            _changed708 = (_changed708) || (!((_old__max_ay24711) == ((_cursor707)._max_ay24)));
            _changed708 = (_changed708) || (!((_old_height712) == ((_cursor707)._height10)));
            _cursor707 = (_cursor707)._parent9;
        }
    }
    var _cursor728 = _parent682;
    var _changed729 = true;
    while ((_changed729) && (!((_cursor728) == (null)))) {
        var _old__min_ax12730 = (_cursor728)._min_ax12;
        var _old__min_ay13731 = (_cursor728)._min_ay13;
        var _old__max_ay24732 = (_cursor728)._max_ay24;
        var _old_height733 = (_cursor728)._height10;
        /* _min_ax12 is min of ax1 */
        var _augval734 = (_cursor728).ax1;
        var _child735 = (_cursor728)._left7;
        if (!((_child735) == null)) {
            var _val736 = (_child735)._min_ax12;
            _augval734 = ((_augval734) < (_val736)) ? (_augval734) : (_val736);
        }
        var _child737 = (_cursor728)._right8;
        if (!((_child737) == null)) {
            var _val738 = (_child737)._min_ax12;
            _augval734 = ((_augval734) < (_val738)) ? (_augval734) : (_val738);
        }
        (_cursor728)._min_ax12 = _augval734;
        /* _min_ay13 is min of ay1 */
        var _augval739 = (_cursor728).ay1;
        var _child740 = (_cursor728)._left7;
        if (!((_child740) == null)) {
            var _val741 = (_child740)._min_ay13;
            _augval739 = ((_augval739) < (_val741)) ? (_augval739) : (_val741);
        }
        var _child742 = (_cursor728)._right8;
        if (!((_child742) == null)) {
            var _val743 = (_child742)._min_ay13;
            _augval739 = ((_augval739) < (_val743)) ? (_augval739) : (_val743);
        }
        (_cursor728)._min_ay13 = _augval739;
        /* _max_ay24 is max of ay2 */
        var _augval744 = (_cursor728).ay2;
        var _child745 = (_cursor728)._left7;
        if (!((_child745) == null)) {
            var _val746 = (_child745)._max_ay24;
            _augval744 = ((_augval744) < (_val746)) ? (_val746) : (_augval744);
        }
        var _child747 = (_cursor728)._right8;
        if (!((_child747) == null)) {
            var _val748 = (_child747)._max_ay24;
            _augval744 = ((_augval744) < (_val748)) ? (_val748) : (_augval744);
        }
        (_cursor728)._max_ay24 = _augval744;
        (_cursor728)._height10 = 1 + ((((((_cursor728)._left7) == null) ? (-1) : (((_cursor728)._left7)._height10)) > ((((_cursor728)._right8) == null) ? (-1) : (((_cursor728)._right8)._height10))) ? ((((_cursor728)._left7) == null) ? (-1) : (((_cursor728)._left7)._height10)) : ((((_cursor728)._right8) == null) ? (-1) : (((_cursor728)._right8)._height10)));
        _changed729 = false;
        _changed729 = (_changed729) || (!((_old__min_ax12730) == ((_cursor728)._min_ax12)));
        _changed729 = (_changed729) || (!((_old__min_ay13731) == ((_cursor728)._min_ay13)));
        _changed729 = (_changed729) || (!((_old__max_ay24732) == ((_cursor728)._max_ay24)));
        _changed729 = (_changed729) || (!((_old_height733) == ((_cursor728)._height10)));
        _cursor728 = (_cursor728)._parent9;
    }
    if (((this)._root1) == (__x)) {
        (this)._root1 = _new_x685;
    }
    (__x)._left7 = null;
    (__x)._right8 = null;
    (__x)._min_ax12 = (__x).ax1;
    (__x)._min_ay13 = (__x).ay1;
    (__x)._max_ay24 = (__x).ay2;
    (__x)._height10 = 0;
    var _previous749 = null;
    var _current750 = (this)._root1;
    var _is_left751 = false;
    while (!((_current750) == null)) {
        _previous749 = _current750;
        if ((ax2) < ((_current750).ax2)) {
            _current750 = (_current750)._left7;
            _is_left751 = true;
        } else {
            _current750 = (_current750)._right8;
            _is_left751 = false;
        }
    }
    if ((_previous749) == null) {
        (this)._root1 = __x;
    } else {
        (__x)._parent9 = _previous749;
        if (_is_left751) {
            (_previous749)._left7 = __x;
        } else {
            (_previous749)._right8 = __x;
        }
    }
    var _cursor752 = (__x)._parent9;
    var _changed753 = true;
    while ((_changed753) && (!((_cursor752) == (null)))) {
        var _old__min_ax12754 = (_cursor752)._min_ax12;
        var _old__min_ay13755 = (_cursor752)._min_ay13;
        var _old__max_ay24756 = (_cursor752)._max_ay24;
        var _old_height757 = (_cursor752)._height10;
        /* _min_ax12 is min of ax1 */
        var _augval758 = (_cursor752).ax1;
        var _child759 = (_cursor752)._left7;
        if (!((_child759) == null)) {
            var _val760 = (_child759)._min_ax12;
            _augval758 = ((_augval758) < (_val760)) ? (_augval758) : (_val760);
        }
        var _child761 = (_cursor752)._right8;
        if (!((_child761) == null)) {
            var _val762 = (_child761)._min_ax12;
            _augval758 = ((_augval758) < (_val762)) ? (_augval758) : (_val762);
        }
        (_cursor752)._min_ax12 = _augval758;
        /* _min_ay13 is min of ay1 */
        var _augval763 = (_cursor752).ay1;
        var _child764 = (_cursor752)._left7;
        if (!((_child764) == null)) {
            var _val765 = (_child764)._min_ay13;
            _augval763 = ((_augval763) < (_val765)) ? (_augval763) : (_val765);
        }
        var _child766 = (_cursor752)._right8;
        if (!((_child766) == null)) {
            var _val767 = (_child766)._min_ay13;
            _augval763 = ((_augval763) < (_val767)) ? (_augval763) : (_val767);
        }
        (_cursor752)._min_ay13 = _augval763;
        /* _max_ay24 is max of ay2 */
        var _augval768 = (_cursor752).ay2;
        var _child769 = (_cursor752)._left7;
        if (!((_child769) == null)) {
            var _val770 = (_child769)._max_ay24;
            _augval768 = ((_augval768) < (_val770)) ? (_val770) : (_augval768);
        }
        var _child771 = (_cursor752)._right8;
        if (!((_child771) == null)) {
            var _val772 = (_child771)._max_ay24;
            _augval768 = ((_augval768) < (_val772)) ? (_val772) : (_augval768);
        }
        (_cursor752)._max_ay24 = _augval768;
        (_cursor752)._height10 = 1 + ((((((_cursor752)._left7) == null) ? (-1) : (((_cursor752)._left7)._height10)) > ((((_cursor752)._right8) == null) ? (-1) : (((_cursor752)._right8)._height10))) ? ((((_cursor752)._left7) == null) ? (-1) : (((_cursor752)._left7)._height10)) : ((((_cursor752)._right8) == null) ? (-1) : (((_cursor752)._right8)._height10)));
        _changed753 = false;
        _changed753 = (_changed753) || (!((_old__min_ax12754) == ((_cursor752)._min_ax12)));
        _changed753 = (_changed753) || (!((_old__min_ay13755) == ((_cursor752)._min_ay13)));
        _changed753 = (_changed753) || (!((_old__max_ay24756) == ((_cursor752)._max_ay24)));
        _changed753 = (_changed753) || (!((_old_height757) == ((_cursor752)._height10)));
        _cursor752 = (_cursor752)._parent9;
    }
    /* rebalance AVL tree */
    var _cursor773 = __x;
    var _imbalance774;
    while (!(((_cursor773)._parent9) == null)) {
        _cursor773 = (_cursor773)._parent9;
        (_cursor773)._height10 = 1 + ((((((_cursor773)._left7) == null) ? (-1) : (((_cursor773)._left7)._height10)) > ((((_cursor773)._right8) == null) ? (-1) : (((_cursor773)._right8)._height10))) ? ((((_cursor773)._left7) == null) ? (-1) : (((_cursor773)._left7)._height10)) : ((((_cursor773)._right8) == null) ? (-1) : (((_cursor773)._right8)._height10)));
        _imbalance774 = ((((_cursor773)._left7) == null) ? (-1) : (((_cursor773)._left7)._height10)) - ((((_cursor773)._right8) == null) ? (-1) : (((_cursor773)._right8)._height10));
        if ((_imbalance774) > (1)) {
            if ((((((_cursor773)._left7)._left7) == null) ? (-1) : ((((_cursor773)._left7)._left7)._height10)) < (((((_cursor773)._left7)._right8) == null) ? (-1) : ((((_cursor773)._left7)._right8)._height10))) {
                /* rotate ((_cursor773)._left7)._right8 */
                var _a775 = (_cursor773)._left7;
                var _b776 = (_a775)._right8;
                var _c777 = (_b776)._left7;
                /* replace _a775 with _b776 in (_a775)._parent9 */
                if (!(((_a775)._parent9) == null)) {
                    if ((((_a775)._parent9)._left7) == (_a775)) {
                        ((_a775)._parent9)._left7 = _b776;
                    } else {
                        ((_a775)._parent9)._right8 = _b776;
                    }
                }
                if (!((_b776) == null)) {
                    (_b776)._parent9 = (_a775)._parent9;
                }
                /* replace _c777 with _a775 in _b776 */
                (_b776)._left7 = _a775;
                if (!((_a775) == null)) {
                    (_a775)._parent9 = _b776;
                }
                /* replace _b776 with _c777 in _a775 */
                (_a775)._right8 = _c777;
                if (!((_c777) == null)) {
                    (_c777)._parent9 = _a775;
                }
                /* _min_ax12 is min of ax1 */
                var _augval778 = (_a775).ax1;
                var _child779 = (_a775)._left7;
                if (!((_child779) == null)) {
                    var _val780 = (_child779)._min_ax12;
                    _augval778 = ((_augval778) < (_val780)) ? (_augval778) : (_val780);
                }
                var _child781 = (_a775)._right8;
                if (!((_child781) == null)) {
                    var _val782 = (_child781)._min_ax12;
                    _augval778 = ((_augval778) < (_val782)) ? (_augval778) : (_val782);
                }
                (_a775)._min_ax12 = _augval778;
                /* _min_ay13 is min of ay1 */
                var _augval783 = (_a775).ay1;
                var _child784 = (_a775)._left7;
                if (!((_child784) == null)) {
                    var _val785 = (_child784)._min_ay13;
                    _augval783 = ((_augval783) < (_val785)) ? (_augval783) : (_val785);
                }
                var _child786 = (_a775)._right8;
                if (!((_child786) == null)) {
                    var _val787 = (_child786)._min_ay13;
                    _augval783 = ((_augval783) < (_val787)) ? (_augval783) : (_val787);
                }
                (_a775)._min_ay13 = _augval783;
                /* _max_ay24 is max of ay2 */
                var _augval788 = (_a775).ay2;
                var _child789 = (_a775)._left7;
                if (!((_child789) == null)) {
                    var _val790 = (_child789)._max_ay24;
                    _augval788 = ((_augval788) < (_val790)) ? (_val790) : (_augval788);
                }
                var _child791 = (_a775)._right8;
                if (!((_child791) == null)) {
                    var _val792 = (_child791)._max_ay24;
                    _augval788 = ((_augval788) < (_val792)) ? (_val792) : (_augval788);
                }
                (_a775)._max_ay24 = _augval788;
                (_a775)._height10 = 1 + ((((((_a775)._left7) == null) ? (-1) : (((_a775)._left7)._height10)) > ((((_a775)._right8) == null) ? (-1) : (((_a775)._right8)._height10))) ? ((((_a775)._left7) == null) ? (-1) : (((_a775)._left7)._height10)) : ((((_a775)._right8) == null) ? (-1) : (((_a775)._right8)._height10)));
                /* _min_ax12 is min of ax1 */
                var _augval793 = (_b776).ax1;
                var _child794 = (_b776)._left7;
                if (!((_child794) == null)) {
                    var _val795 = (_child794)._min_ax12;
                    _augval793 = ((_augval793) < (_val795)) ? (_augval793) : (_val795);
                }
                var _child796 = (_b776)._right8;
                if (!((_child796) == null)) {
                    var _val797 = (_child796)._min_ax12;
                    _augval793 = ((_augval793) < (_val797)) ? (_augval793) : (_val797);
                }
                (_b776)._min_ax12 = _augval793;
                /* _min_ay13 is min of ay1 */
                var _augval798 = (_b776).ay1;
                var _child799 = (_b776)._left7;
                if (!((_child799) == null)) {
                    var _val800 = (_child799)._min_ay13;
                    _augval798 = ((_augval798) < (_val800)) ? (_augval798) : (_val800);
                }
                var _child801 = (_b776)._right8;
                if (!((_child801) == null)) {
                    var _val802 = (_child801)._min_ay13;
                    _augval798 = ((_augval798) < (_val802)) ? (_augval798) : (_val802);
                }
                (_b776)._min_ay13 = _augval798;
                /* _max_ay24 is max of ay2 */
                var _augval803 = (_b776).ay2;
                var _child804 = (_b776)._left7;
                if (!((_child804) == null)) {
                    var _val805 = (_child804)._max_ay24;
                    _augval803 = ((_augval803) < (_val805)) ? (_val805) : (_augval803);
                }
                var _child806 = (_b776)._right8;
                if (!((_child806) == null)) {
                    var _val807 = (_child806)._max_ay24;
                    _augval803 = ((_augval803) < (_val807)) ? (_val807) : (_augval803);
                }
                (_b776)._max_ay24 = _augval803;
                (_b776)._height10 = 1 + ((((((_b776)._left7) == null) ? (-1) : (((_b776)._left7)._height10)) > ((((_b776)._right8) == null) ? (-1) : (((_b776)._right8)._height10))) ? ((((_b776)._left7) == null) ? (-1) : (((_b776)._left7)._height10)) : ((((_b776)._right8) == null) ? (-1) : (((_b776)._right8)._height10)));
                if (!(((_b776)._parent9) == null)) {
                    /* _min_ax12 is min of ax1 */
                    var _augval808 = ((_b776)._parent9).ax1;
                    var _child809 = ((_b776)._parent9)._left7;
                    if (!((_child809) == null)) {
                        var _val810 = (_child809)._min_ax12;
                        _augval808 = ((_augval808) < (_val810)) ? (_augval808) : (_val810);
                    }
                    var _child811 = ((_b776)._parent9)._right8;
                    if (!((_child811) == null)) {
                        var _val812 = (_child811)._min_ax12;
                        _augval808 = ((_augval808) < (_val812)) ? (_augval808) : (_val812);
                    }
                    ((_b776)._parent9)._min_ax12 = _augval808;
                    /* _min_ay13 is min of ay1 */
                    var _augval813 = ((_b776)._parent9).ay1;
                    var _child814 = ((_b776)._parent9)._left7;
                    if (!((_child814) == null)) {
                        var _val815 = (_child814)._min_ay13;
                        _augval813 = ((_augval813) < (_val815)) ? (_augval813) : (_val815);
                    }
                    var _child816 = ((_b776)._parent9)._right8;
                    if (!((_child816) == null)) {
                        var _val817 = (_child816)._min_ay13;
                        _augval813 = ((_augval813) < (_val817)) ? (_augval813) : (_val817);
                    }
                    ((_b776)._parent9)._min_ay13 = _augval813;
                    /* _max_ay24 is max of ay2 */
                    var _augval818 = ((_b776)._parent9).ay2;
                    var _child819 = ((_b776)._parent9)._left7;
                    if (!((_child819) == null)) {
                        var _val820 = (_child819)._max_ay24;
                        _augval818 = ((_augval818) < (_val820)) ? (_val820) : (_augval818);
                    }
                    var _child821 = ((_b776)._parent9)._right8;
                    if (!((_child821) == null)) {
                        var _val822 = (_child821)._max_ay24;
                        _augval818 = ((_augval818) < (_val822)) ? (_val822) : (_augval818);
                    }
                    ((_b776)._parent9)._max_ay24 = _augval818;
                    ((_b776)._parent9)._height10 = 1 + (((((((_b776)._parent9)._left7) == null) ? (-1) : ((((_b776)._parent9)._left7)._height10)) > (((((_b776)._parent9)._right8) == null) ? (-1) : ((((_b776)._parent9)._right8)._height10))) ? (((((_b776)._parent9)._left7) == null) ? (-1) : ((((_b776)._parent9)._left7)._height10)) : (((((_b776)._parent9)._right8) == null) ? (-1) : ((((_b776)._parent9)._right8)._height10)));
                } else {
                    (this)._root1 = _b776;
                }
            }
            /* rotate (_cursor773)._left7 */
            var _a823 = _cursor773;
            var _b824 = (_a823)._left7;
            var _c825 = (_b824)._right8;
            /* replace _a823 with _b824 in (_a823)._parent9 */
            if (!(((_a823)._parent9) == null)) {
                if ((((_a823)._parent9)._left7) == (_a823)) {
                    ((_a823)._parent9)._left7 = _b824;
                } else {
                    ((_a823)._parent9)._right8 = _b824;
                }
            }
            if (!((_b824) == null)) {
                (_b824)._parent9 = (_a823)._parent9;
            }
            /* replace _c825 with _a823 in _b824 */
            (_b824)._right8 = _a823;
            if (!((_a823) == null)) {
                (_a823)._parent9 = _b824;
            }
            /* replace _b824 with _c825 in _a823 */
            (_a823)._left7 = _c825;
            if (!((_c825) == null)) {
                (_c825)._parent9 = _a823;
            }
            /* _min_ax12 is min of ax1 */
            var _augval826 = (_a823).ax1;
            var _child827 = (_a823)._left7;
            if (!((_child827) == null)) {
                var _val828 = (_child827)._min_ax12;
                _augval826 = ((_augval826) < (_val828)) ? (_augval826) : (_val828);
            }
            var _child829 = (_a823)._right8;
            if (!((_child829) == null)) {
                var _val830 = (_child829)._min_ax12;
                _augval826 = ((_augval826) < (_val830)) ? (_augval826) : (_val830);
            }
            (_a823)._min_ax12 = _augval826;
            /* _min_ay13 is min of ay1 */
            var _augval831 = (_a823).ay1;
            var _child832 = (_a823)._left7;
            if (!((_child832) == null)) {
                var _val833 = (_child832)._min_ay13;
                _augval831 = ((_augval831) < (_val833)) ? (_augval831) : (_val833);
            }
            var _child834 = (_a823)._right8;
            if (!((_child834) == null)) {
                var _val835 = (_child834)._min_ay13;
                _augval831 = ((_augval831) < (_val835)) ? (_augval831) : (_val835);
            }
            (_a823)._min_ay13 = _augval831;
            /* _max_ay24 is max of ay2 */
            var _augval836 = (_a823).ay2;
            var _child837 = (_a823)._left7;
            if (!((_child837) == null)) {
                var _val838 = (_child837)._max_ay24;
                _augval836 = ((_augval836) < (_val838)) ? (_val838) : (_augval836);
            }
            var _child839 = (_a823)._right8;
            if (!((_child839) == null)) {
                var _val840 = (_child839)._max_ay24;
                _augval836 = ((_augval836) < (_val840)) ? (_val840) : (_augval836);
            }
            (_a823)._max_ay24 = _augval836;
            (_a823)._height10 = 1 + ((((((_a823)._left7) == null) ? (-1) : (((_a823)._left7)._height10)) > ((((_a823)._right8) == null) ? (-1) : (((_a823)._right8)._height10))) ? ((((_a823)._left7) == null) ? (-1) : (((_a823)._left7)._height10)) : ((((_a823)._right8) == null) ? (-1) : (((_a823)._right8)._height10)));
            /* _min_ax12 is min of ax1 */
            var _augval841 = (_b824).ax1;
            var _child842 = (_b824)._left7;
            if (!((_child842) == null)) {
                var _val843 = (_child842)._min_ax12;
                _augval841 = ((_augval841) < (_val843)) ? (_augval841) : (_val843);
            }
            var _child844 = (_b824)._right8;
            if (!((_child844) == null)) {
                var _val845 = (_child844)._min_ax12;
                _augval841 = ((_augval841) < (_val845)) ? (_augval841) : (_val845);
            }
            (_b824)._min_ax12 = _augval841;
            /* _min_ay13 is min of ay1 */
            var _augval846 = (_b824).ay1;
            var _child847 = (_b824)._left7;
            if (!((_child847) == null)) {
                var _val848 = (_child847)._min_ay13;
                _augval846 = ((_augval846) < (_val848)) ? (_augval846) : (_val848);
            }
            var _child849 = (_b824)._right8;
            if (!((_child849) == null)) {
                var _val850 = (_child849)._min_ay13;
                _augval846 = ((_augval846) < (_val850)) ? (_augval846) : (_val850);
            }
            (_b824)._min_ay13 = _augval846;
            /* _max_ay24 is max of ay2 */
            var _augval851 = (_b824).ay2;
            var _child852 = (_b824)._left7;
            if (!((_child852) == null)) {
                var _val853 = (_child852)._max_ay24;
                _augval851 = ((_augval851) < (_val853)) ? (_val853) : (_augval851);
            }
            var _child854 = (_b824)._right8;
            if (!((_child854) == null)) {
                var _val855 = (_child854)._max_ay24;
                _augval851 = ((_augval851) < (_val855)) ? (_val855) : (_augval851);
            }
            (_b824)._max_ay24 = _augval851;
            (_b824)._height10 = 1 + ((((((_b824)._left7) == null) ? (-1) : (((_b824)._left7)._height10)) > ((((_b824)._right8) == null) ? (-1) : (((_b824)._right8)._height10))) ? ((((_b824)._left7) == null) ? (-1) : (((_b824)._left7)._height10)) : ((((_b824)._right8) == null) ? (-1) : (((_b824)._right8)._height10)));
            if (!(((_b824)._parent9) == null)) {
                /* _min_ax12 is min of ax1 */
                var _augval856 = ((_b824)._parent9).ax1;
                var _child857 = ((_b824)._parent9)._left7;
                if (!((_child857) == null)) {
                    var _val858 = (_child857)._min_ax12;
                    _augval856 = ((_augval856) < (_val858)) ? (_augval856) : (_val858);
                }
                var _child859 = ((_b824)._parent9)._right8;
                if (!((_child859) == null)) {
                    var _val860 = (_child859)._min_ax12;
                    _augval856 = ((_augval856) < (_val860)) ? (_augval856) : (_val860);
                }
                ((_b824)._parent9)._min_ax12 = _augval856;
                /* _min_ay13 is min of ay1 */
                var _augval861 = ((_b824)._parent9).ay1;
                var _child862 = ((_b824)._parent9)._left7;
                if (!((_child862) == null)) {
                    var _val863 = (_child862)._min_ay13;
                    _augval861 = ((_augval861) < (_val863)) ? (_augval861) : (_val863);
                }
                var _child864 = ((_b824)._parent9)._right8;
                if (!((_child864) == null)) {
                    var _val865 = (_child864)._min_ay13;
                    _augval861 = ((_augval861) < (_val865)) ? (_augval861) : (_val865);
                }
                ((_b824)._parent9)._min_ay13 = _augval861;
                /* _max_ay24 is max of ay2 */
                var _augval866 = ((_b824)._parent9).ay2;
                var _child867 = ((_b824)._parent9)._left7;
                if (!((_child867) == null)) {
                    var _val868 = (_child867)._max_ay24;
                    _augval866 = ((_augval866) < (_val868)) ? (_val868) : (_augval866);
                }
                var _child869 = ((_b824)._parent9)._right8;
                if (!((_child869) == null)) {
                    var _val870 = (_child869)._max_ay24;
                    _augval866 = ((_augval866) < (_val870)) ? (_val870) : (_augval866);
                }
                ((_b824)._parent9)._max_ay24 = _augval866;
                ((_b824)._parent9)._height10 = 1 + (((((((_b824)._parent9)._left7) == null) ? (-1) : ((((_b824)._parent9)._left7)._height10)) > (((((_b824)._parent9)._right8) == null) ? (-1) : ((((_b824)._parent9)._right8)._height10))) ? (((((_b824)._parent9)._left7) == null) ? (-1) : ((((_b824)._parent9)._left7)._height10)) : (((((_b824)._parent9)._right8) == null) ? (-1) : ((((_b824)._parent9)._right8)._height10)));
            } else {
                (this)._root1 = _b824;
            }
            _cursor773 = (_cursor773)._parent9;
        } else if ((_imbalance774) < (-1)) {
            if ((((((_cursor773)._right8)._left7) == null) ? (-1) : ((((_cursor773)._right8)._left7)._height10)) > (((((_cursor773)._right8)._right8) == null) ? (-1) : ((((_cursor773)._right8)._right8)._height10))) {
                /* rotate ((_cursor773)._right8)._left7 */
                var _a871 = (_cursor773)._right8;
                var _b872 = (_a871)._left7;
                var _c873 = (_b872)._right8;
                /* replace _a871 with _b872 in (_a871)._parent9 */
                if (!(((_a871)._parent9) == null)) {
                    if ((((_a871)._parent9)._left7) == (_a871)) {
                        ((_a871)._parent9)._left7 = _b872;
                    } else {
                        ((_a871)._parent9)._right8 = _b872;
                    }
                }
                if (!((_b872) == null)) {
                    (_b872)._parent9 = (_a871)._parent9;
                }
                /* replace _c873 with _a871 in _b872 */
                (_b872)._right8 = _a871;
                if (!((_a871) == null)) {
                    (_a871)._parent9 = _b872;
                }
                /* replace _b872 with _c873 in _a871 */
                (_a871)._left7 = _c873;
                if (!((_c873) == null)) {
                    (_c873)._parent9 = _a871;
                }
                /* _min_ax12 is min of ax1 */
                var _augval874 = (_a871).ax1;
                var _child875 = (_a871)._left7;
                if (!((_child875) == null)) {
                    var _val876 = (_child875)._min_ax12;
                    _augval874 = ((_augval874) < (_val876)) ? (_augval874) : (_val876);
                }
                var _child877 = (_a871)._right8;
                if (!((_child877) == null)) {
                    var _val878 = (_child877)._min_ax12;
                    _augval874 = ((_augval874) < (_val878)) ? (_augval874) : (_val878);
                }
                (_a871)._min_ax12 = _augval874;
                /* _min_ay13 is min of ay1 */
                var _augval879 = (_a871).ay1;
                var _child880 = (_a871)._left7;
                if (!((_child880) == null)) {
                    var _val881 = (_child880)._min_ay13;
                    _augval879 = ((_augval879) < (_val881)) ? (_augval879) : (_val881);
                }
                var _child882 = (_a871)._right8;
                if (!((_child882) == null)) {
                    var _val883 = (_child882)._min_ay13;
                    _augval879 = ((_augval879) < (_val883)) ? (_augval879) : (_val883);
                }
                (_a871)._min_ay13 = _augval879;
                /* _max_ay24 is max of ay2 */
                var _augval884 = (_a871).ay2;
                var _child885 = (_a871)._left7;
                if (!((_child885) == null)) {
                    var _val886 = (_child885)._max_ay24;
                    _augval884 = ((_augval884) < (_val886)) ? (_val886) : (_augval884);
                }
                var _child887 = (_a871)._right8;
                if (!((_child887) == null)) {
                    var _val888 = (_child887)._max_ay24;
                    _augval884 = ((_augval884) < (_val888)) ? (_val888) : (_augval884);
                }
                (_a871)._max_ay24 = _augval884;
                (_a871)._height10 = 1 + ((((((_a871)._left7) == null) ? (-1) : (((_a871)._left7)._height10)) > ((((_a871)._right8) == null) ? (-1) : (((_a871)._right8)._height10))) ? ((((_a871)._left7) == null) ? (-1) : (((_a871)._left7)._height10)) : ((((_a871)._right8) == null) ? (-1) : (((_a871)._right8)._height10)));
                /* _min_ax12 is min of ax1 */
                var _augval889 = (_b872).ax1;
                var _child890 = (_b872)._left7;
                if (!((_child890) == null)) {
                    var _val891 = (_child890)._min_ax12;
                    _augval889 = ((_augval889) < (_val891)) ? (_augval889) : (_val891);
                }
                var _child892 = (_b872)._right8;
                if (!((_child892) == null)) {
                    var _val893 = (_child892)._min_ax12;
                    _augval889 = ((_augval889) < (_val893)) ? (_augval889) : (_val893);
                }
                (_b872)._min_ax12 = _augval889;
                /* _min_ay13 is min of ay1 */
                var _augval894 = (_b872).ay1;
                var _child895 = (_b872)._left7;
                if (!((_child895) == null)) {
                    var _val896 = (_child895)._min_ay13;
                    _augval894 = ((_augval894) < (_val896)) ? (_augval894) : (_val896);
                }
                var _child897 = (_b872)._right8;
                if (!((_child897) == null)) {
                    var _val898 = (_child897)._min_ay13;
                    _augval894 = ((_augval894) < (_val898)) ? (_augval894) : (_val898);
                }
                (_b872)._min_ay13 = _augval894;
                /* _max_ay24 is max of ay2 */
                var _augval899 = (_b872).ay2;
                var _child900 = (_b872)._left7;
                if (!((_child900) == null)) {
                    var _val901 = (_child900)._max_ay24;
                    _augval899 = ((_augval899) < (_val901)) ? (_val901) : (_augval899);
                }
                var _child902 = (_b872)._right8;
                if (!((_child902) == null)) {
                    var _val903 = (_child902)._max_ay24;
                    _augval899 = ((_augval899) < (_val903)) ? (_val903) : (_augval899);
                }
                (_b872)._max_ay24 = _augval899;
                (_b872)._height10 = 1 + ((((((_b872)._left7) == null) ? (-1) : (((_b872)._left7)._height10)) > ((((_b872)._right8) == null) ? (-1) : (((_b872)._right8)._height10))) ? ((((_b872)._left7) == null) ? (-1) : (((_b872)._left7)._height10)) : ((((_b872)._right8) == null) ? (-1) : (((_b872)._right8)._height10)));
                if (!(((_b872)._parent9) == null)) {
                    /* _min_ax12 is min of ax1 */
                    var _augval904 = ((_b872)._parent9).ax1;
                    var _child905 = ((_b872)._parent9)._left7;
                    if (!((_child905) == null)) {
                        var _val906 = (_child905)._min_ax12;
                        _augval904 = ((_augval904) < (_val906)) ? (_augval904) : (_val906);
                    }
                    var _child907 = ((_b872)._parent9)._right8;
                    if (!((_child907) == null)) {
                        var _val908 = (_child907)._min_ax12;
                        _augval904 = ((_augval904) < (_val908)) ? (_augval904) : (_val908);
                    }
                    ((_b872)._parent9)._min_ax12 = _augval904;
                    /* _min_ay13 is min of ay1 */
                    var _augval909 = ((_b872)._parent9).ay1;
                    var _child910 = ((_b872)._parent9)._left7;
                    if (!((_child910) == null)) {
                        var _val911 = (_child910)._min_ay13;
                        _augval909 = ((_augval909) < (_val911)) ? (_augval909) : (_val911);
                    }
                    var _child912 = ((_b872)._parent9)._right8;
                    if (!((_child912) == null)) {
                        var _val913 = (_child912)._min_ay13;
                        _augval909 = ((_augval909) < (_val913)) ? (_augval909) : (_val913);
                    }
                    ((_b872)._parent9)._min_ay13 = _augval909;
                    /* _max_ay24 is max of ay2 */
                    var _augval914 = ((_b872)._parent9).ay2;
                    var _child915 = ((_b872)._parent9)._left7;
                    if (!((_child915) == null)) {
                        var _val916 = (_child915)._max_ay24;
                        _augval914 = ((_augval914) < (_val916)) ? (_val916) : (_augval914);
                    }
                    var _child917 = ((_b872)._parent9)._right8;
                    if (!((_child917) == null)) {
                        var _val918 = (_child917)._max_ay24;
                        _augval914 = ((_augval914) < (_val918)) ? (_val918) : (_augval914);
                    }
                    ((_b872)._parent9)._max_ay24 = _augval914;
                    ((_b872)._parent9)._height10 = 1 + (((((((_b872)._parent9)._left7) == null) ? (-1) : ((((_b872)._parent9)._left7)._height10)) > (((((_b872)._parent9)._right8) == null) ? (-1) : ((((_b872)._parent9)._right8)._height10))) ? (((((_b872)._parent9)._left7) == null) ? (-1) : ((((_b872)._parent9)._left7)._height10)) : (((((_b872)._parent9)._right8) == null) ? (-1) : ((((_b872)._parent9)._right8)._height10)));
                } else {
                    (this)._root1 = _b872;
                }
            }
            /* rotate (_cursor773)._right8 */
            var _a919 = _cursor773;
            var _b920 = (_a919)._right8;
            var _c921 = (_b920)._left7;
            /* replace _a919 with _b920 in (_a919)._parent9 */
            if (!(((_a919)._parent9) == null)) {
                if ((((_a919)._parent9)._left7) == (_a919)) {
                    ((_a919)._parent9)._left7 = _b920;
                } else {
                    ((_a919)._parent9)._right8 = _b920;
                }
            }
            if (!((_b920) == null)) {
                (_b920)._parent9 = (_a919)._parent9;
            }
            /* replace _c921 with _a919 in _b920 */
            (_b920)._left7 = _a919;
            if (!((_a919) == null)) {
                (_a919)._parent9 = _b920;
            }
            /* replace _b920 with _c921 in _a919 */
            (_a919)._right8 = _c921;
            if (!((_c921) == null)) {
                (_c921)._parent9 = _a919;
            }
            /* _min_ax12 is min of ax1 */
            var _augval922 = (_a919).ax1;
            var _child923 = (_a919)._left7;
            if (!((_child923) == null)) {
                var _val924 = (_child923)._min_ax12;
                _augval922 = ((_augval922) < (_val924)) ? (_augval922) : (_val924);
            }
            var _child925 = (_a919)._right8;
            if (!((_child925) == null)) {
                var _val926 = (_child925)._min_ax12;
                _augval922 = ((_augval922) < (_val926)) ? (_augval922) : (_val926);
            }
            (_a919)._min_ax12 = _augval922;
            /* _min_ay13 is min of ay1 */
            var _augval927 = (_a919).ay1;
            var _child928 = (_a919)._left7;
            if (!((_child928) == null)) {
                var _val929 = (_child928)._min_ay13;
                _augval927 = ((_augval927) < (_val929)) ? (_augval927) : (_val929);
            }
            var _child930 = (_a919)._right8;
            if (!((_child930) == null)) {
                var _val931 = (_child930)._min_ay13;
                _augval927 = ((_augval927) < (_val931)) ? (_augval927) : (_val931);
            }
            (_a919)._min_ay13 = _augval927;
            /* _max_ay24 is max of ay2 */
            var _augval932 = (_a919).ay2;
            var _child933 = (_a919)._left7;
            if (!((_child933) == null)) {
                var _val934 = (_child933)._max_ay24;
                _augval932 = ((_augval932) < (_val934)) ? (_val934) : (_augval932);
            }
            var _child935 = (_a919)._right8;
            if (!((_child935) == null)) {
                var _val936 = (_child935)._max_ay24;
                _augval932 = ((_augval932) < (_val936)) ? (_val936) : (_augval932);
            }
            (_a919)._max_ay24 = _augval932;
            (_a919)._height10 = 1 + ((((((_a919)._left7) == null) ? (-1) : (((_a919)._left7)._height10)) > ((((_a919)._right8) == null) ? (-1) : (((_a919)._right8)._height10))) ? ((((_a919)._left7) == null) ? (-1) : (((_a919)._left7)._height10)) : ((((_a919)._right8) == null) ? (-1) : (((_a919)._right8)._height10)));
            /* _min_ax12 is min of ax1 */
            var _augval937 = (_b920).ax1;
            var _child938 = (_b920)._left7;
            if (!((_child938) == null)) {
                var _val939 = (_child938)._min_ax12;
                _augval937 = ((_augval937) < (_val939)) ? (_augval937) : (_val939);
            }
            var _child940 = (_b920)._right8;
            if (!((_child940) == null)) {
                var _val941 = (_child940)._min_ax12;
                _augval937 = ((_augval937) < (_val941)) ? (_augval937) : (_val941);
            }
            (_b920)._min_ax12 = _augval937;
            /* _min_ay13 is min of ay1 */
            var _augval942 = (_b920).ay1;
            var _child943 = (_b920)._left7;
            if (!((_child943) == null)) {
                var _val944 = (_child943)._min_ay13;
                _augval942 = ((_augval942) < (_val944)) ? (_augval942) : (_val944);
            }
            var _child945 = (_b920)._right8;
            if (!((_child945) == null)) {
                var _val946 = (_child945)._min_ay13;
                _augval942 = ((_augval942) < (_val946)) ? (_augval942) : (_val946);
            }
            (_b920)._min_ay13 = _augval942;
            /* _max_ay24 is max of ay2 */
            var _augval947 = (_b920).ay2;
            var _child948 = (_b920)._left7;
            if (!((_child948) == null)) {
                var _val949 = (_child948)._max_ay24;
                _augval947 = ((_augval947) < (_val949)) ? (_val949) : (_augval947);
            }
            var _child950 = (_b920)._right8;
            if (!((_child950) == null)) {
                var _val951 = (_child950)._max_ay24;
                _augval947 = ((_augval947) < (_val951)) ? (_val951) : (_augval947);
            }
            (_b920)._max_ay24 = _augval947;
            (_b920)._height10 = 1 + ((((((_b920)._left7) == null) ? (-1) : (((_b920)._left7)._height10)) > ((((_b920)._right8) == null) ? (-1) : (((_b920)._right8)._height10))) ? ((((_b920)._left7) == null) ? (-1) : (((_b920)._left7)._height10)) : ((((_b920)._right8) == null) ? (-1) : (((_b920)._right8)._height10)));
            if (!(((_b920)._parent9) == null)) {
                /* _min_ax12 is min of ax1 */
                var _augval952 = ((_b920)._parent9).ax1;
                var _child953 = ((_b920)._parent9)._left7;
                if (!((_child953) == null)) {
                    var _val954 = (_child953)._min_ax12;
                    _augval952 = ((_augval952) < (_val954)) ? (_augval952) : (_val954);
                }
                var _child955 = ((_b920)._parent9)._right8;
                if (!((_child955) == null)) {
                    var _val956 = (_child955)._min_ax12;
                    _augval952 = ((_augval952) < (_val956)) ? (_augval952) : (_val956);
                }
                ((_b920)._parent9)._min_ax12 = _augval952;
                /* _min_ay13 is min of ay1 */
                var _augval957 = ((_b920)._parent9).ay1;
                var _child958 = ((_b920)._parent9)._left7;
                if (!((_child958) == null)) {
                    var _val959 = (_child958)._min_ay13;
                    _augval957 = ((_augval957) < (_val959)) ? (_augval957) : (_val959);
                }
                var _child960 = ((_b920)._parent9)._right8;
                if (!((_child960) == null)) {
                    var _val961 = (_child960)._min_ay13;
                    _augval957 = ((_augval957) < (_val961)) ? (_augval957) : (_val961);
                }
                ((_b920)._parent9)._min_ay13 = _augval957;
                /* _max_ay24 is max of ay2 */
                var _augval962 = ((_b920)._parent9).ay2;
                var _child963 = ((_b920)._parent9)._left7;
                if (!((_child963) == null)) {
                    var _val964 = (_child963)._max_ay24;
                    _augval962 = ((_augval962) < (_val964)) ? (_val964) : (_augval962);
                }
                var _child965 = ((_b920)._parent9)._right8;
                if (!((_child965) == null)) {
                    var _val966 = (_child965)._max_ay24;
                    _augval962 = ((_augval962) < (_val966)) ? (_val966) : (_augval962);
                }
                ((_b920)._parent9)._max_ay24 = _augval962;
                ((_b920)._parent9)._height10 = 1 + (((((((_b920)._parent9)._left7) == null) ? (-1) : ((((_b920)._parent9)._left7)._height10)) > (((((_b920)._parent9)._right8) == null) ? (-1) : ((((_b920)._parent9)._right8)._height10))) ? (((((_b920)._parent9)._left7) == null) ? (-1) : ((((_b920)._parent9)._left7)._height10)) : (((((_b920)._parent9)._right8) == null) ? (-1) : ((((_b920)._parent9)._right8)._height10)));
            } else {
                (this)._root1 = _b920;
            }
            _cursor773 = (_cursor773)._parent9;
        }
    }
    (__x).ax1 = ax1;
    (__x).ay1 = ay1;
    (__x).ax2 = ax2;
    (__x).ay2 = ay2;
}
RectangleHolder.prototype.findMatchingRectangles = function (bx1, by1, bx2, by2, __callback) {
    var _root967 = (this)._root1;
    var _x968 = _root967;
    var _descend969 = true;
    var _from_left970 = true;
    while (true) {
        if ((_x968) == null) {
            _x968 = null;
            break;
        }
        if (_descend969) {
            /* too small? */
            if ((false) || (((_x968).ax2) <= (bx1))) {
                if ((!(((_x968)._right8) == null)) && ((((true) && ((((_x968)._right8)._min_ax12) < (bx2))) && ((((_x968)._right8)._min_ay13) < (by2))) && ((((_x968)._right8)._max_ay24) > (by1)))) {
                    if ((_x968) == (_root967)) {
                        _root967 = (_x968)._right8;
                    }
                    _x968 = (_x968)._right8;
                } else if ((_x968) == (_root967)) {
                    _x968 = null;
                    break;
                } else {
                    _descend969 = false;
                    _from_left970 = (!(((_x968)._parent9) == null)) && ((_x968) == (((_x968)._parent9)._left7));
                    _x968 = (_x968)._parent9;
                }
            } else if ((!(((_x968)._left7) == null)) && ((((true) && ((((_x968)._left7)._min_ax12) < (bx2))) && ((((_x968)._left7)._min_ay13) < (by2))) && ((((_x968)._left7)._max_ay24) > (by1)))) {
                _x968 = (_x968)._left7;
                /* too large? */
            } else if (false) {
                if ((_x968) == (_root967)) {
                    _x968 = null;
                    break;
                } else {
                    _descend969 = false;
                    _from_left970 = (!(((_x968)._parent9) == null)) && ((_x968) == (((_x968)._parent9)._left7));
                    _x968 = (_x968)._parent9;
                }
                /* node ok? */
            } else if ((((true) && (((_x968).ax1) < (bx2))) && (((_x968).ay1) < (by2))) && (((_x968).ay2) > (by1))) {
                break;
            } else if ((_x968) == (_root967)) {
                _root967 = (_x968)._right8;
                _x968 = (_x968)._right8;
            } else {
                if ((!(((_x968)._right8) == null)) && ((((true) && ((((_x968)._right8)._min_ax12) < (bx2))) && ((((_x968)._right8)._min_ay13) < (by2))) && ((((_x968)._right8)._max_ay24) > (by1)))) {
                    if ((_x968) == (_root967)) {
                        _root967 = (_x968)._right8;
                    }
                    _x968 = (_x968)._right8;
                } else {
                    _descend969 = false;
                    _from_left970 = (!(((_x968)._parent9) == null)) && ((_x968) == (((_x968)._parent9)._left7));
                    _x968 = (_x968)._parent9;
                }
            }
        } else if (_from_left970) {
            if (false) {
                _x968 = null;
                break;
            } else if ((((true) && (((_x968).ax1) < (bx2))) && (((_x968).ay1) < (by2))) && (((_x968).ay2) > (by1))) {
                break;
            } else if ((!(((_x968)._right8) == null)) && ((((true) && ((((_x968)._right8)._min_ax12) < (bx2))) && ((((_x968)._right8)._min_ay13) < (by2))) && ((((_x968)._right8)._max_ay24) > (by1)))) {
                _descend969 = true;
                if ((_x968) == (_root967)) {
                    _root967 = (_x968)._right8;
                }
                _x968 = (_x968)._right8;
            } else if ((_x968) == (_root967)) {
                _x968 = null;
                break;
            } else {
                _descend969 = false;
                _from_left970 = (!(((_x968)._parent9) == null)) && ((_x968) == (((_x968)._parent9)._left7));
                _x968 = (_x968)._parent9;
            }
        } else {
            if ((_x968) == (_root967)) {
                _x968 = null;
                break;
            } else {
                _descend969 = false;
                _from_left970 = (!(((_x968)._parent9) == null)) && ((_x968) == (((_x968)._parent9)._left7));
                _x968 = (_x968)._parent9;
            }
        }
    }
    var _prev_cursor5 = null;
    var _cursor6 = _x968;
    for (; ;) {
        if (!(!((_cursor6) == null))) break;
        var _name971 = _cursor6;
        /* ADVANCE */
        _prev_cursor5 = _cursor6;
        do {
            var _right_min972 = null;
            if ((!(((_cursor6)._right8) == null)) && ((((true) && ((((_cursor6)._right8)._min_ax12) < (bx2))) && ((((_cursor6)._right8)._min_ay13) < (by2))) && ((((_cursor6)._right8)._max_ay24) > (by1)))) {
                var _root973 = (_cursor6)._right8;
                var _x974 = _root973;
                var _descend975 = true;
                var _from_left976 = true;
                while (true) {
                    if ((_x974) == null) {
                        _x974 = null;
                        break;
                    }
                    if (_descend975) {
                        /* too small? */
                        if ((false) || (((_x974).ax2) <= (bx1))) {
                            if ((!(((_x974)._right8) == null)) && ((((true) && ((((_x974)._right8)._min_ax12) < (bx2))) && ((((_x974)._right8)._min_ay13) < (by2))) && ((((_x974)._right8)._max_ay24) > (by1)))) {
                                if ((_x974) == (_root973)) {
                                    _root973 = (_x974)._right8;
                                }
                                _x974 = (_x974)._right8;
                            } else if ((_x974) == (_root973)) {
                                _x974 = null;
                                break;
                            } else {
                                _descend975 = false;
                                _from_left976 = (!(((_x974)._parent9) == null)) && ((_x974) == (((_x974)._parent9)._left7));
                                _x974 = (_x974)._parent9;
                            }
                        } else if ((!(((_x974)._left7) == null)) && ((((true) && ((((_x974)._left7)._min_ax12) < (bx2))) && ((((_x974)._left7)._min_ay13) < (by2))) && ((((_x974)._left7)._max_ay24) > (by1)))) {
                            _x974 = (_x974)._left7;
                            /* too large? */
                        } else if (false) {
                            if ((_x974) == (_root973)) {
                                _x974 = null;
                                break;
                            } else {
                                _descend975 = false;
                                _from_left976 = (!(((_x974)._parent9) == null)) && ((_x974) == (((_x974)._parent9)._left7));
                                _x974 = (_x974)._parent9;
                            }
                            /* node ok? */
                        } else if ((((true) && (((_x974).ax1) < (bx2))) && (((_x974).ay1) < (by2))) && (((_x974).ay2) > (by1))) {
                            break;
                        } else if ((_x974) == (_root973)) {
                            _root973 = (_x974)._right8;
                            _x974 = (_x974)._right8;
                        } else {
                            if ((!(((_x974)._right8) == null)) && ((((true) && ((((_x974)._right8)._min_ax12) < (bx2))) && ((((_x974)._right8)._min_ay13) < (by2))) && ((((_x974)._right8)._max_ay24) > (by1)))) {
                                if ((_x974) == (_root973)) {
                                    _root973 = (_x974)._right8;
                                }
                                _x974 = (_x974)._right8;
                            } else {
                                _descend975 = false;
                                _from_left976 = (!(((_x974)._parent9) == null)) && ((_x974) == (((_x974)._parent9)._left7));
                                _x974 = (_x974)._parent9;
                            }
                        }
                    } else if (_from_left976) {
                        if (false) {
                            _x974 = null;
                            break;
                        } else if ((((true) && (((_x974).ax1) < (bx2))) && (((_x974).ay1) < (by2))) && (((_x974).ay2) > (by1))) {
                            break;
                        } else if ((!(((_x974)._right8) == null)) && ((((true) && ((((_x974)._right8)._min_ax12) < (bx2))) && ((((_x974)._right8)._min_ay13) < (by2))) && ((((_x974)._right8)._max_ay24) > (by1)))) {
                            _descend975 = true;
                            if ((_x974) == (_root973)) {
                                _root973 = (_x974)._right8;
                            }
                            _x974 = (_x974)._right8;
                        } else if ((_x974) == (_root973)) {
                            _x974 = null;
                            break;
                        } else {
                            _descend975 = false;
                            _from_left976 = (!(((_x974)._parent9) == null)) && ((_x974) == (((_x974)._parent9)._left7));
                            _x974 = (_x974)._parent9;
                        }
                    } else {
                        if ((_x974) == (_root973)) {
                            _x974 = null;
                            break;
                        } else {
                            _descend975 = false;
                            _from_left976 = (!(((_x974)._parent9) == null)) && ((_x974) == (((_x974)._parent9)._left7));
                            _x974 = (_x974)._parent9;
                        }
                    }
                }
                _right_min972 = _x974;
            }
            if (!((_right_min972) == null)) {
                _cursor6 = _right_min972;
                break;
            } else {
                while ((!(((_cursor6)._parent9) == null)) && ((_cursor6) == (((_cursor6)._parent9)._right8))) {
                    _cursor6 = (_cursor6)._parent9;
                }
                _cursor6 = (_cursor6)._parent9;
                if ((!((_cursor6) == null)) && (false)) {
                    _cursor6 = null;
                }
            }
        } while ((!((_cursor6) == null)) && (!((((true) && (((_cursor6).ax1) < (bx2))) && (((_cursor6).ay1) < (by2))) && (((_cursor6).ay2) > (by1)))));
        if (__callback(_name971)) {
            var _to_remove977 = _prev_cursor5;
            var _parent978 = (_to_remove977)._parent9;
            var _left979 = (_to_remove977)._left7;
            var _right980 = (_to_remove977)._right8;
            var _new_x981;
            if (((_left979) == null) && ((_right980) == null)) {
                _new_x981 = null;
                /* replace _to_remove977 with _new_x981 in _parent978 */
                if (!((_parent978) == null)) {
                    if (((_parent978)._left7) == (_to_remove977)) {
                        (_parent978)._left7 = _new_x981;
                    } else {
                        (_parent978)._right8 = _new_x981;
                    }
                }
                if (!((_new_x981) == null)) {
                    (_new_x981)._parent9 = _parent978;
                }
            } else if ((!((_left979) == null)) && ((_right980) == null)) {
                _new_x981 = _left979;
                /* replace _to_remove977 with _new_x981 in _parent978 */
                if (!((_parent978) == null)) {
                    if (((_parent978)._left7) == (_to_remove977)) {
                        (_parent978)._left7 = _new_x981;
                    } else {
                        (_parent978)._right8 = _new_x981;
                    }
                }
                if (!((_new_x981) == null)) {
                    (_new_x981)._parent9 = _parent978;
                }
            } else if (((_left979) == null) && (!((_right980) == null))) {
                _new_x981 = _right980;
                /* replace _to_remove977 with _new_x981 in _parent978 */
                if (!((_parent978) == null)) {
                    if (((_parent978)._left7) == (_to_remove977)) {
                        (_parent978)._left7 = _new_x981;
                    } else {
                        (_parent978)._right8 = _new_x981;
                    }
                }
                if (!((_new_x981) == null)) {
                    (_new_x981)._parent9 = _parent978;
                }
            } else {
                var _root982 = (_to_remove977)._right8;
                var _x983 = _root982;
                var _descend984 = true;
                var _from_left985 = true;
                while (true) {
                    if ((_x983) == null) {
                        _x983 = null;
                        break;
                    }
                    if (_descend984) {
                        /* too small? */
                        if (false) {
                            if ((!(((_x983)._right8) == null)) && (true)) {
                                if ((_x983) == (_root982)) {
                                    _root982 = (_x983)._right8;
                                }
                                _x983 = (_x983)._right8;
                            } else if ((_x983) == (_root982)) {
                                _x983 = null;
                                break;
                            } else {
                                _descend984 = false;
                                _from_left985 = (!(((_x983)._parent9) == null)) && ((_x983) == (((_x983)._parent9)._left7));
                                _x983 = (_x983)._parent9;
                            }
                        } else if ((!(((_x983)._left7) == null)) && (true)) {
                            _x983 = (_x983)._left7;
                            /* too large? */
                        } else if (false) {
                            if ((_x983) == (_root982)) {
                                _x983 = null;
                                break;
                            } else {
                                _descend984 = false;
                                _from_left985 = (!(((_x983)._parent9) == null)) && ((_x983) == (((_x983)._parent9)._left7));
                                _x983 = (_x983)._parent9;
                            }
                            /* node ok? */
                        } else if (true) {
                            break;
                        } else if ((_x983) == (_root982)) {
                            _root982 = (_x983)._right8;
                            _x983 = (_x983)._right8;
                        } else {
                            if ((!(((_x983)._right8) == null)) && (true)) {
                                if ((_x983) == (_root982)) {
                                    _root982 = (_x983)._right8;
                                }
                                _x983 = (_x983)._right8;
                            } else {
                                _descend984 = false;
                                _from_left985 = (!(((_x983)._parent9) == null)) && ((_x983) == (((_x983)._parent9)._left7));
                                _x983 = (_x983)._parent9;
                            }
                        }
                    } else if (_from_left985) {
                        if (false) {
                            _x983 = null;
                            break;
                        } else if (true) {
                            break;
                        } else if ((!(((_x983)._right8) == null)) && (true)) {
                            _descend984 = true;
                            if ((_x983) == (_root982)) {
                                _root982 = (_x983)._right8;
                            }
                            _x983 = (_x983)._right8;
                        } else if ((_x983) == (_root982)) {
                            _x983 = null;
                            break;
                        } else {
                            _descend984 = false;
                            _from_left985 = (!(((_x983)._parent9) == null)) && ((_x983) == (((_x983)._parent9)._left7));
                            _x983 = (_x983)._parent9;
                        }
                    } else {
                        if ((_x983) == (_root982)) {
                            _x983 = null;
                            break;
                        } else {
                            _descend984 = false;
                            _from_left985 = (!(((_x983)._parent9) == null)) && ((_x983) == (((_x983)._parent9)._left7));
                            _x983 = (_x983)._parent9;
                        }
                    }
                }
                _new_x981 = _x983;
                var _mp986 = (_x983)._parent9;
                var _mr987 = (_x983)._right8;
                /* replace _x983 with _mr987 in _mp986 */
                if (!((_mp986) == null)) {
                    if (((_mp986)._left7) == (_x983)) {
                        (_mp986)._left7 = _mr987;
                    } else {
                        (_mp986)._right8 = _mr987;
                    }
                }
                if (!((_mr987) == null)) {
                    (_mr987)._parent9 = _mp986;
                }
                /* replace _to_remove977 with _x983 in _parent978 */
                if (!((_parent978) == null)) {
                    if (((_parent978)._left7) == (_to_remove977)) {
                        (_parent978)._left7 = _x983;
                    } else {
                        (_parent978)._right8 = _x983;
                    }
                }
                if (!((_x983) == null)) {
                    (_x983)._parent9 = _parent978;
                }
                /* replace null with _left979 in _x983 */
                (_x983)._left7 = _left979;
                if (!((_left979) == null)) {
                    (_left979)._parent9 = _x983;
                }
                /* replace _mr987 with (_to_remove977)._right8 in _x983 */
                (_x983)._right8 = (_to_remove977)._right8;
                if (!(((_to_remove977)._right8) == null)) {
                    ((_to_remove977)._right8)._parent9 = _x983;
                }
                /* _min_ax12 is min of ax1 */
                var _augval988 = (_x983).ax1;
                var _child989 = (_x983)._left7;
                if (!((_child989) == null)) {
                    var _val990 = (_child989)._min_ax12;
                    _augval988 = ((_augval988) < (_val990)) ? (_augval988) : (_val990);
                }
                var _child991 = (_x983)._right8;
                if (!((_child991) == null)) {
                    var _val992 = (_child991)._min_ax12;
                    _augval988 = ((_augval988) < (_val992)) ? (_augval988) : (_val992);
                }
                (_x983)._min_ax12 = _augval988;
                /* _min_ay13 is min of ay1 */
                var _augval993 = (_x983).ay1;
                var _child994 = (_x983)._left7;
                if (!((_child994) == null)) {
                    var _val995 = (_child994)._min_ay13;
                    _augval993 = ((_augval993) < (_val995)) ? (_augval993) : (_val995);
                }
                var _child996 = (_x983)._right8;
                if (!((_child996) == null)) {
                    var _val997 = (_child996)._min_ay13;
                    _augval993 = ((_augval993) < (_val997)) ? (_augval993) : (_val997);
                }
                (_x983)._min_ay13 = _augval993;
                /* _max_ay24 is max of ay2 */
                var _augval998 = (_x983).ay2;
                var _child999 = (_x983)._left7;
                if (!((_child999) == null)) {
                    var _val1000 = (_child999)._max_ay24;
                    _augval998 = ((_augval998) < (_val1000)) ? (_val1000) : (_augval998);
                }
                var _child1001 = (_x983)._right8;
                if (!((_child1001) == null)) {
                    var _val1002 = (_child1001)._max_ay24;
                    _augval998 = ((_augval998) < (_val1002)) ? (_val1002) : (_augval998);
                }
                (_x983)._max_ay24 = _augval998;
                (_x983)._height10 = 1 + ((((((_x983)._left7) == null) ? (-1) : (((_x983)._left7)._height10)) > ((((_x983)._right8) == null) ? (-1) : (((_x983)._right8)._height10))) ? ((((_x983)._left7) == null) ? (-1) : (((_x983)._left7)._height10)) : ((((_x983)._right8) == null) ? (-1) : (((_x983)._right8)._height10)));
                var _cursor1003 = _mp986;
                var _changed1004 = true;
                while ((_changed1004) && (!((_cursor1003) == (_parent978)))) {
                    var _old__min_ax121005 = (_cursor1003)._min_ax12;
                    var _old__min_ay131006 = (_cursor1003)._min_ay13;
                    var _old__max_ay241007 = (_cursor1003)._max_ay24;
                    var _old_height1008 = (_cursor1003)._height10;
                    /* _min_ax12 is min of ax1 */
                    var _augval1009 = (_cursor1003).ax1;
                    var _child1010 = (_cursor1003)._left7;
                    if (!((_child1010) == null)) {
                        var _val1011 = (_child1010)._min_ax12;
                        _augval1009 = ((_augval1009) < (_val1011)) ? (_augval1009) : (_val1011);
                    }
                    var _child1012 = (_cursor1003)._right8;
                    if (!((_child1012) == null)) {
                        var _val1013 = (_child1012)._min_ax12;
                        _augval1009 = ((_augval1009) < (_val1013)) ? (_augval1009) : (_val1013);
                    }
                    (_cursor1003)._min_ax12 = _augval1009;
                    /* _min_ay13 is min of ay1 */
                    var _augval1014 = (_cursor1003).ay1;
                    var _child1015 = (_cursor1003)._left7;
                    if (!((_child1015) == null)) {
                        var _val1016 = (_child1015)._min_ay13;
                        _augval1014 = ((_augval1014) < (_val1016)) ? (_augval1014) : (_val1016);
                    }
                    var _child1017 = (_cursor1003)._right8;
                    if (!((_child1017) == null)) {
                        var _val1018 = (_child1017)._min_ay13;
                        _augval1014 = ((_augval1014) < (_val1018)) ? (_augval1014) : (_val1018);
                    }
                    (_cursor1003)._min_ay13 = _augval1014;
                    /* _max_ay24 is max of ay2 */
                    var _augval1019 = (_cursor1003).ay2;
                    var _child1020 = (_cursor1003)._left7;
                    if (!((_child1020) == null)) {
                        var _val1021 = (_child1020)._max_ay24;
                        _augval1019 = ((_augval1019) < (_val1021)) ? (_val1021) : (_augval1019);
                    }
                    var _child1022 = (_cursor1003)._right8;
                    if (!((_child1022) == null)) {
                        var _val1023 = (_child1022)._max_ay24;
                        _augval1019 = ((_augval1019) < (_val1023)) ? (_val1023) : (_augval1019);
                    }
                    (_cursor1003)._max_ay24 = _augval1019;
                    (_cursor1003)._height10 = 1 + ((((((_cursor1003)._left7) == null) ? (-1) : (((_cursor1003)._left7)._height10)) > ((((_cursor1003)._right8) == null) ? (-1) : (((_cursor1003)._right8)._height10))) ? ((((_cursor1003)._left7) == null) ? (-1) : (((_cursor1003)._left7)._height10)) : ((((_cursor1003)._right8) == null) ? (-1) : (((_cursor1003)._right8)._height10)));
                    _changed1004 = false;
                    _changed1004 = (_changed1004) || (!((_old__min_ax121005) == ((_cursor1003)._min_ax12)));
                    _changed1004 = (_changed1004) || (!((_old__min_ay131006) == ((_cursor1003)._min_ay13)));
                    _changed1004 = (_changed1004) || (!((_old__max_ay241007) == ((_cursor1003)._max_ay24)));
                    _changed1004 = (_changed1004) || (!((_old_height1008) == ((_cursor1003)._height10)));
                    _cursor1003 = (_cursor1003)._parent9;
                }
            }
            var _cursor1024 = _parent978;
            var _changed1025 = true;
            while ((_changed1025) && (!((_cursor1024) == (null)))) {
                var _old__min_ax121026 = (_cursor1024)._min_ax12;
                var _old__min_ay131027 = (_cursor1024)._min_ay13;
                var _old__max_ay241028 = (_cursor1024)._max_ay24;
                var _old_height1029 = (_cursor1024)._height10;
                /* _min_ax12 is min of ax1 */
                var _augval1030 = (_cursor1024).ax1;
                var _child1031 = (_cursor1024)._left7;
                if (!((_child1031) == null)) {
                    var _val1032 = (_child1031)._min_ax12;
                    _augval1030 = ((_augval1030) < (_val1032)) ? (_augval1030) : (_val1032);
                }
                var _child1033 = (_cursor1024)._right8;
                if (!((_child1033) == null)) {
                    var _val1034 = (_child1033)._min_ax12;
                    _augval1030 = ((_augval1030) < (_val1034)) ? (_augval1030) : (_val1034);
                }
                (_cursor1024)._min_ax12 = _augval1030;
                /* _min_ay13 is min of ay1 */
                var _augval1035 = (_cursor1024).ay1;
                var _child1036 = (_cursor1024)._left7;
                if (!((_child1036) == null)) {
                    var _val1037 = (_child1036)._min_ay13;
                    _augval1035 = ((_augval1035) < (_val1037)) ? (_augval1035) : (_val1037);
                }
                var _child1038 = (_cursor1024)._right8;
                if (!((_child1038) == null)) {
                    var _val1039 = (_child1038)._min_ay13;
                    _augval1035 = ((_augval1035) < (_val1039)) ? (_augval1035) : (_val1039);
                }
                (_cursor1024)._min_ay13 = _augval1035;
                /* _max_ay24 is max of ay2 */
                var _augval1040 = (_cursor1024).ay2;
                var _child1041 = (_cursor1024)._left7;
                if (!((_child1041) == null)) {
                    var _val1042 = (_child1041)._max_ay24;
                    _augval1040 = ((_augval1040) < (_val1042)) ? (_val1042) : (_augval1040);
                }
                var _child1043 = (_cursor1024)._right8;
                if (!((_child1043) == null)) {
                    var _val1044 = (_child1043)._max_ay24;
                    _augval1040 = ((_augval1040) < (_val1044)) ? (_val1044) : (_augval1040);
                }
                (_cursor1024)._max_ay24 = _augval1040;
                (_cursor1024)._height10 = 1 + ((((((_cursor1024)._left7) == null) ? (-1) : (((_cursor1024)._left7)._height10)) > ((((_cursor1024)._right8) == null) ? (-1) : (((_cursor1024)._right8)._height10))) ? ((((_cursor1024)._left7) == null) ? (-1) : (((_cursor1024)._left7)._height10)) : ((((_cursor1024)._right8) == null) ? (-1) : (((_cursor1024)._right8)._height10)));
                _changed1025 = false;
                _changed1025 = (_changed1025) || (!((_old__min_ax121026) == ((_cursor1024)._min_ax12)));
                _changed1025 = (_changed1025) || (!((_old__min_ay131027) == ((_cursor1024)._min_ay13)));
                _changed1025 = (_changed1025) || (!((_old__max_ay241028) == ((_cursor1024)._max_ay24)));
                _changed1025 = (_changed1025) || (!((_old_height1029) == ((_cursor1024)._height10)));
                _cursor1024 = (_cursor1024)._parent9;
            }
            if (((this)._root1) == (_to_remove977)) {
                (this)._root1 = _new_x981;
            }
            _prev_cursor5 = null;
        }
    };
}
; 
 
 buildViz = function (d3) {
    return function (widthInPixels = 1000,
                     heightInPixels = 600,
                     max_snippets = null,
                     color = null,
                     sortByDist = true,
                     useFullDoc = false,
                     greyZeroScores = false,
                     asianMode = false,
                     nonTextFeaturesMode = false,
                     showCharacteristic = true,
                     wordVecMaxPValue = false,
                     saveSvgButton = false,
                     reverseSortScoresForNotCategory = false,
                     minPVal = 0.1,
                     pValueColors = false,
                     xLabelText = null,
                     yLabelText = null,
                     fullData = null,
                     showTopTerms = true,
                     showNeutral = false,
                     getTooltipContent = null,
                     xAxisValues = null,
                     yAxisValues = null,
                     colorFunc = null,
                     showAxes = true,
                     showExtra = false,
                     doCensorPoints = true,
                     centerLabelsOverPoints = false,
                     xAxisLabels = null,
                     yAxisLabels = null,
                     topic_model_preview_size = 10,
                     verticalLines = null,
                     horizontal_line_y_position = null,
                     vertical_line_x_position = null,
                     unifiedContexts = false,
                     showCategoryHeadings = true,
                     showCrossAxes = true,
                     divName = 'd3-div-1',
                     alternativeTermFunc = null,
                     includeAllContexts = false,
                     showAxesAndCrossHairs = false,
                     x_axis_values_format = '.3f',
                     y_axis_values_format = '.3f',
                     matchFullLine = false,
                     maxOverlapping = -1,
                     showCorpusStats = true,
                     sortDocLabelsByName = false) {
        //var divName = 'd3-div-1';
        // Set the dimensions of the canvas / graph
        var padding = {top: 30, right: 20, bottom: 30, left: 50};
        if (!showAxes) {
            padding = {top: 30, right: 20, bottom: 30, left: 50};
        }
        var margin = padding,
            width = widthInPixels - margin.left - margin.right,
            height = heightInPixels - margin.top - margin.bottom;
        fullData.data.forEach(function (x, i) {
            x.i = i
        });

        // Set the ranges
        var x = d3.scaleLinear().range([0, width]);
        var y = d3.scaleLinear().range([height, 0]);

        if (unifiedContexts) {
            document.querySelectorAll('#' + divName + '-' + 'notcol')
                .forEach(function (x) {
                    x.style.display = 'none'
                });
            document.querySelectorAll('.' + divName + '-' + 'contexts')
                .forEach(function (x) {
                    x.style.width = '90%'
                });
        } else if (showNeutral) {
            if (showExtra) {
                document.querySelectorAll('.' + divName + '-' + 'contexts')
                    .forEach(function (x) {
                        x.style.width = '25%'
                        x.style.float = 'left'
                    });

                ['notcol', 'neutcol', 'extracol'].forEach(function (columnName) {
                    document.querySelectorAll('#' + divName + '-' + columnName)
                        .forEach(function (x) {
                            x.style.display = 'inline'
                            x.style.float = 'left'
                            x.style.width = '25%'
                        });
                })

            } else {
                document.querySelectorAll('.' + divName + '-' + 'contexts')
                    .forEach(function (x) {
                        x.style.width = '33%'
                        x.style.float = 'left'
                    });

                ['notcol', 'neutcol'].forEach(function (columnName) {
                    document.querySelectorAll('#' + divName + '-' + columnName)
                        .forEach(function (x) {
                            x.style.display = 'inline'
                            x.style.float = 'left'
                            x.style.width = '33%'
                        });
                })


            }
        } else {
            document.querySelectorAll('.' + divName + '-' + 'contexts')
                .forEach(function (x) {
                    x.style.width = '45%'
                    //x.style.display = 'inline'
                    x.style.float = 'left'
                });

            ['notcol'].forEach(function (columnName) {
                document.querySelectorAll('#' + divName + '-' + columnName)
                    .forEach(function (x) {
                        //x.style.display = 'inline'
                        x.style.float = 'left'
                        x.style.width = '45%'
                    });
            })
        }

        var yAxis = null;
        var xAxis = null;

        function axisLabelerFactory(axis) {
            if ((axis == "x" && xLabelText == null)
                || (axis == "y" && yLabelText == null))
                return function (d, i) {
                    return ["Infrequent", "Average", "Frequent"][i];
                };

            return function (d, i) {
                return ["Low", "Medium", "High"][i];
            }
        }


        function bs(ar, x) {
            function bsa(s, e) {
                var mid = Math.floor((s + e) / 2);
                var midval = ar[mid];
                if (s == e) {
                    return s;
                }
                if (midval == x) {
                    return mid;
                } else if (midval < x) {
                    return bsa(mid + 1, e);
                } else {
                    return bsa(s, mid);
                }
            }

            return bsa(0, ar.length);
        }


        console.log("fullData");
        console.log(fullData);


        var sortedX = fullData.data.map(x => x).sort(function (a, b) {
            return a.x < b.x ? -1 : (a.x == b.x ? 0 : 1);
        }).map(function (x) {
            return x.x
        });

        var sortedOx = fullData.data.map(x => x).sort(function (a, b) {
            return a.ox < b.ox ? -1 : (a.ox == b.ox ? 0 : 1);
        }).map(function (x) {
            return x.ox
        });

        var sortedY = fullData.data.map(x => x).sort(function (a, b) {
            return a.y < b.y ? -1 : (a.y == b.y ? 0 : 1);
        }).map(function (x) {
            return x.y
        });

        var sortedOy = fullData.data.map(x => x).sort(function (a, b) {
            return a.oy < b.oy ? -1 : (a.oy == b.oy ? 0 : 1);
        }).map(function (x) {
            return x.oy
        });
        console.log(fullData.data[0])

        function labelWithZScore(axis, axisName, tickPoints, axis_values_format) {
            var myVals = axisName === 'x' ? sortedOx : sortedOy;
            var myPlotedVals = axisName === 'x' ? sortedX : sortedY;
            var ticks = tickPoints.map(function (x) {
                return myPlotedVals[bs(myVals, x)]
            });
            return axis.tickValues(ticks).tickFormat(
                function (d, i) {
                    return d3.format(axis_values_format)(tickPoints[i]);
                })
        }

        if (xAxisValues) {
            xAxis = labelWithZScore(d3.axisBottom(x), 'x', xAxisValues, x_axis_values_format);
        } else if (xAxisLabels) {
            xAxis = d3.axisBottom(x)
                .ticks(xAxisLabels.length)
                .tickFormat(function (d, i) {
                    return xAxisLabels[i];
                });
        } else {
            xAxis = d3.axisBottom(x).ticks(3).tickFormat(axisLabelerFactory('x'));
        }
        if (yAxisValues) {
            yAxis = labelWithZScore(d3.axisLeft(y), 'y', yAxisValues, y_axis_values_format);
        } else if (yAxisLabels) {
            yAxis = d3.axisLeft(y)
                .ticks(yAxisLabels.length)
                .tickFormat(function (d, i) {
                    return yAxisLabels[i];
                });
        } else {
            yAxis = d3.axisLeft(y).ticks(3).tickFormat(axisLabelerFactory('y'));
        }

        // var label = d3.select("body").append("div")
        var label = d3.select('#' + divName).append("div")
            .attr("class", "label");


        var interpolateLightGreys = d3.interpolate(d3.rgb(230, 230, 230),
            d3.rgb(130, 130, 130));
        // setup fill color
        if (color == null) {
            color = d3.interpolateRdYlBu;
            //color = d3.interpolateWarm;
        }

        var pixelsToAddToWidth = 200;
        if (!showTopTerms && !showCharacteristic) {
            pixelsToAddToWidth = 0;
        }

        // Adds the svg canvas
        // var svg = d3.select("body")
        svg = d3.select('#' + divName)
            .append("svg")
            .attr("width", width + margin.left + margin.right + pixelsToAddToWidth)
            .attr("height", height + margin.top + margin.bottom)
            .append("g")
            .attr("transform",
                "translate(" + margin.left + "," + margin.top + ")");


        origSVGLeft = svg.node().getBoundingClientRect().left;
        origSVGTop = svg.node().getBoundingClientRect().top;
        var lastCircleSelected = null;

        function getCorpusWordCounts() {
            var binaryLabels = fullData.docs.labels.map(function (label) {
                return 1 * (fullData.docs.categories[label] != fullData.info.category_internal_name);
            });
            var wordCounts = {}; // word -> [cat counts, not-cat-counts]
            var wordCountSums = [0, 0];
            fullData.docs.texts.forEach(function (text, i) {
                text.toLowerCase().trim().split(/\W+/).forEach(function (word) {
                    if (word.trim() !== '') {
                        if (!(word in wordCounts))
                            wordCounts[word] = [0, 0];
                        wordCounts[word][binaryLabels[i]]++;
                        wordCountSums[binaryLabels[i]]++;
                    }
                })
            });
            return {
                avgDocLen: (wordCountSums[0] + wordCountSums[1]) / fullData.docs.texts.length,
                counts: wordCounts,
                sums: wordCountSums,
                uniques: [[0, 0]].concat(Object.keys(wordCounts).map(function (key) {
                    return wordCounts[key];
                })).reduce(function (a, b) {
                    return [a[0] + (b[0] > 0), a[1] + (b[1] > 0)]
                })
            };
        }

        function getContextWordCounts(query) {
            var wordCounts = {};
            var wordCountSums = [0, 0];
            var priorCountSums = [0, 0];
            gatherTermContexts(termDict[query])
                .contexts
                .forEach(function (contextSet, categoryIdx) {
                    contextSet.forEach(function (context) {
                        context.snippets.forEach(function (snippet) {
                            var tokens = snippet.toLowerCase().trim().replace('<b>', '').replace('</b>', '').split(/\W+/);
                            var matchIndices = [];
                            tokens.forEach(function (word, i) {
                                if (word === query) matchIndices.push(i)
                            });
                            tokens.forEach(function (word, i) {
                                if (word.trim() !== '') {
                                    var isValid = false;
                                    for (var matchI in matchIndices) {
                                        if (Math.abs(i - matchI) < 3) {
                                            isValid = true;
                                            break
                                        }
                                    }
                                    if (isValid) {
                                        //console.log([word, i, matchI, isValid]);
                                        if (!(word in wordCounts)) {
                                            var priorCounts = corpusWordCounts.counts[word]
                                            wordCounts[word] = [0, 0].concat(priorCounts);
                                            priorCountSums[0] += priorCounts[0];
                                            priorCountSums[1] += priorCounts[1];
                                        }
                                        wordCounts[word][categoryIdx]++;
                                        wordCountSums[categoryIdx]++;
                                    }
                                }
                            })
                        })
                    })
                });
            return {
                counts: wordCounts,
                priorSums: priorCountSums,
                sums: wordCountSums,
                uniques: [[0, 0]].concat(Object.keys(wordCounts).map(function (key) {
                    return wordCounts[key];
                })).reduce(function (a, b) {
                    return [a[0] + (b[0] > 0), a[1] + (b[1] > 0)];
                })
            }

        }

        function denseRank(ar) {
            var markedAr = ar.map((x, i) => [x, i]).sort((a, b) => a[0] - b[0]);
            var curRank = 1
            var rankedAr = markedAr.map(
                function (x, i) {
                    if (i > 0 && x[0] != markedAr[i - 1][0]) {
                        curRank++;
                    }
                    return [curRank, x[0], x[1]];
                }
            )
            return rankedAr.map(x => x).sort((a, b) => (a[2] - b[2])).map(x => x[0]);
        }


        function getDenseRanks(fullData, categoryNum) {
            var fgFreqs = Array(fullData.data.length).fill(0);
            var bgFreqs = Array(fullData.data.length).fill(0);
            var categoryTermCounts = fullData.termCounts[categoryNum];


            Object.keys(categoryTermCounts).forEach(
                key => fgFreqs[key] = categoryTermCounts[key][0]
            )
            fullData.termCounts.forEach(
                function (categoryTermCounts, otherCategoryNum) {
                    if (otherCategoryNum != categoryNum) {
                        Object.keys(categoryTermCounts).forEach(
                            key => bgFreqs[key] += categoryTermCounts[key][0]
                        )
                    }
                }
            )
            var fgDenseRanks = denseRank(fgFreqs);
            var bgDenseRanks = denseRank(bgFreqs);

            var maxfgDenseRanks = Math.max(...fgDenseRanks);
            var minfgDenseRanks = Math.min(...fgDenseRanks);
            var scalefgDenseRanks = fgDenseRanks.map(
                x => (x - minfgDenseRanks) / (maxfgDenseRanks - minfgDenseRanks)
            )

            var maxbgDenseRanks = Math.max(...bgDenseRanks);
            var minbgDenseRanks = Math.min(...bgDenseRanks);
            var scalebgDenseRanks = bgDenseRanks.map(
                x => (x - minbgDenseRanks) / (maxbgDenseRanks - minbgDenseRanks)
            )

            return {'fg': scalefgDenseRanks, 'bg': scalebgDenseRanks, 'bgFreqs': bgFreqs, 'fgFreqs': fgFreqs}
        }

        function getCategoryDenseRankScores(fullData, categoryNum) {
            var denseRanks = getDenseRanks(fullData, categoryNum)
            return denseRanks.fg.map((x, i) => x - denseRanks.bg[i]);
        }

        function getTermCounts(fullData) {
            var counts = Array(fullData.data.length).fill(0);
            fullData.termCounts.forEach(
                function (categoryTermCounts) {
                    Object.keys(categoryTermCounts).forEach(
                        key => counts[key] = categoryTermCounts[key][0]
                    )
                }
            )
            return counts;
        }

        function getContextWordLORIPs(query) {
            var contextWordCounts = getContextWordCounts(query);
            var ni_k = contextWordCounts.sums[0];
            var nj_k = contextWordCounts.sums[1];
            var n = ni_k + nj_k;
            //var ai_k0 = contextWordCounts.priorSums[0] + contextWordCounts.priorSums[1];
            //var aj_k0 = contextWordCounts.priorSums[0] + contextWordCounts.priorSums[1];
            var a0 = 0.00001 //corpusWordCounts.avgDocLen;
            var a_k0 = Object.keys(contextWordCounts.counts)
                .map(function (x) {
                    var counts = contextWordCounts.counts[x];
                    return a0 * (counts[2] + counts[3]) /
                        (contextWordCounts.priorSums[0] + contextWordCounts.priorSums[1]);
                })
                .reduce(function (a, b) {
                    return a + b
                });
            var ai_k0 = a_k0 / ni_k;
            var aj_k0 = a_k0 / nj_k;
            var scores = Object.keys(contextWordCounts.counts).map(
                function (word) {
                    var countData = contextWordCounts.counts[word];
                    var yi = countData[0];
                    var yj = countData[1];
                    //var ai = countData[2];
                    //var aj = countData[3];
                    //var ai = countData[2] + countData[3];
                    //var aj = ai;
                    //var ai = (countData[2] + countData[3]) * a0/ni_k;
                    //var aj = (countData[2] + countData[3]) * a0/nj_k;
                    var ai = a0 * (countData[2] + countData[3]) /
                        (contextWordCounts.priorSums[0] + contextWordCounts.priorSums[1]);
                    var aj = ai;
                    var deltahat_i_j =
                        +Math.log((yi + ai) * 1. / (ni_k + ai_k0 - yi - ai))
                        - Math.log((yj + aj) * 1. / (nj_k + aj_k0 - yj - aj));
                    var var_deltahat_i_j = 1. / (yi + ai) + 1. / (ni_k + ai_k0 - yi - ai)
                        + 1. / (yj + aj) + 1. / (nj_k + aj_k0 - yj - aj);
                    var zeta_ij = deltahat_i_j / Math.sqrt(var_deltahat_i_j);
                    return [word, yi, yj, ai, aj, ai_k0, zeta_ij];
                }
            ).sort(function (a, b) {
                return b[5] - a[5];
            });
            return scores;
        }

        function getContextWordSFS(query) {
            // from https://stackoverflow.com/questions/14846767/std-normal-cdf-normal-cdf-or-error-function
            function cdf(x, mean, variance) {
                return 0.5 * (1 + erf((x - mean) / (Math.sqrt(2 * variance))));
            }

            function erf(x) {
                // save the sign of x
                var sign = (x >= 0) ? 1 : -1;
                x = Math.abs(x);

                // constants
                var a1 = 0.254829592;
                var a2 = -0.284496736;
                var a3 = 1.421413741;
                var a4 = -1.453152027;
                var a5 = 1.061405429;
                var p = 0.3275911;

                // A&S formula 7.1.26
                var t = 1.0 / (1.0 + p * x);
                var y = 1.0 - (((((a5 * t + a4) * t) + a3) * t + a2) * t + a1) * t * Math.exp(-x * x);
                return sign * y; // erf(-x) = -erf(x);
            }

            function scale(a) {
                return Math.log(a + 0.0000001);
            }

            var contextWordCounts = getContextWordCounts(query);
            var wordList = Object.keys(contextWordCounts.counts).map(function (word) {
                return contextWordCounts.counts[word].concat([word]);
            });
            var cat_freq_xbar = wordList.map(function (x) {
                return scale(x[0])
            }).reduce(function (a, b) {
                return a + b
            }) / wordList.length;
            var cat_freq_var = wordList.map(function (x) {
                return Math.pow((scale(x[0]) - cat_freq_xbar), 2);
            }).reduce(function (a, b) {
                return a + b
            }) / wordList.length;
            var cat_prec_xbar = wordList.map(function (x) {
                return scale(x[0] / (x[0] + x[1]));
            }).reduce(function (a, b) {
                return a + b
            }) / wordList.length;
            var cat_prec_var = wordList.map(function (x) {
                return Math.pow((scale(x[0] / (x[0] + x[1])) - cat_prec_xbar), 2);
            }).reduce(function (a, b) {
                return a + b
            }) / wordList.length;

            var ncat_freq_xbar = wordList.map(function (x) {
                return scale(x[0])
            }).reduce(function (a, b) {
                return a + b
            }) / wordList.length;
            var ncat_freq_var = wordList.map(function (x) {
                return Math.pow((scale(x[0]) - ncat_freq_xbar), 2);
            }).reduce(function (a, b) {
                return a + b
            }) / wordList.length;
            var ncat_prec_xbar = wordList.map(function (x) {
                return scale(x[0] / (x[0] + x[1]));
            }).reduce(function (a, b) {
                return a + b
            }) / wordList.length;
            var ncat_prec_var = wordList.map(function (x) {
                return Math.pow((scale(x[0] / (x[0] + x[1])) - ncat_prec_xbar), 2);
            }).reduce(function (a, b) {
                return a + b
            }) / wordList.length;

            function scaledFScore(cnt, other, freq_xbar, freq_var, prec_xbar, prec_var) {
                var beta = 1.5;
                var normFreq = cdf(scale(cnt), freq_xbar, freq_var);
                var normPrec = cdf(scale(cnt / (cnt + other)), prec_xbar, prec_var);
                return (1 + Math.pow(beta, 2)) * normFreq * normPrec / (Math.pow(beta, 2) * normFreq + normPrec);
            }

            var sfs = wordList.map(function (x) {
                cat_sfs = scaledFScore(x[0], x[1], cat_freq_xbar,
                    cat_freq_var, cat_prec_xbar, cat_prec_var);
                ncat_sfs = scaledFScore(x[1], x[0], ncat_freq_xbar,
                    ncat_freq_var, ncat_prec_xbar, ncat_prec_var);
                return [cat_sfs > ncat_sfs ? cat_sfs : -ncat_sfs].concat(x);

            }).sort(function (a, b) {
                return b[0] - a[0];
            });
            return sfs;
        }

        function deselectLastCircle() {
            if (lastCircleSelected) {
                lastCircleSelected.style["stroke"] = null;
                lastCircleSelected = null;
            }
        }

        function getSentenceBoundaries(text) {
            // !!! need to use spacy's sentence splitter
            if (asianMode) {
                var sentenceRe = /\n/gmi;
            } else {
                var sentenceRe = /\(?[^\.\?\!\n\b]+[\n\.!\?]\)?/g;
            }
            var offsets = [];
            var match;
            while ((match = sentenceRe.exec(text)) != null) {
                offsets.push(match.index);
            }
            offsets.push(text.length);
            return offsets;
        }

        function getMatchingSnippet(text, boundaries, start, end) {
            var sentenceStart = null;
            var sentenceEnd = null;
            for (var i in boundaries) {
                var position = boundaries[i];
                if (position <= start && (sentenceStart == null || position > sentenceStart)) {
                    sentenceStart = position;
                }
                if (position >= end) {
                    sentenceEnd = position;
                    break;
                }
            }
            var snippet = (text.slice(sentenceStart, start) + "<b>" + text.slice(start, end)
                + "</b>" + text.slice(end, sentenceEnd)).trim();
            if (sentenceStart == null) {
                sentenceStart = 0;
            }
            return {'snippet': snippet, 'sentenceStart': sentenceStart};
        }

        function gatherTermContexts(d, includeAll = true) {
            var category_name = fullData['info']['category_name'];
            var not_category_name = fullData['info']['not_category_name'];
            var matches = [[], [], [], []];
            console.log("searching")

            if (fullData.docs === undefined) return matches;
            if (!nonTextFeaturesMode) {
                return searchInText(d, includeAll);
            } else {
                return searchInExtraFeatures(d, includeAll);
            }
        }

        function searchInExtraFeatures(d) {
            var matches = [[], [], [], []];
            var term = d.term;
            var categoryNum = fullData.docs.categories.indexOf(fullData.info.category_internal_name);
            var notCategoryNumList = fullData.docs.categories.map(function (x, i) {
                if (fullData.info.not_category_internal_names.indexOf(x) > -1) {
                    return i;
                } else {
                    return -1;
                }
            }).filter(function (x) {
                return x > -1
            });
            var neutralCategoryNumList = fullData.docs.categories.map(function (x, i) {
                if (fullData.info.neutral_category_internal_names.indexOf(x) > -1) {
                    return i;
                } else {
                    return -1;
                }
            }).filter(function (x) {
                return x > -1
            });
            var extraCategoryNumList = fullData.docs.categories.map(function (x, i) {
                if (fullData.info.extra_category_internal_names.indexOf(x) > -1) {
                    return i;
                } else {
                    return -1;
                }
            }).filter(function (x) {
                return x > -1
            });

            var pattern = null;
            if ('metalists' in fullData && term in fullData.metalists) {
                // from https://stackoverflow.com/questions/3446170/escape-string-for-use-in-javascript-regex
                function escapeRegExp(str) {
                    return str.replace(/[\-\[\]\/\{\}\(\)\*\+\?\.\\\^\$\|\']/g, "\\$&");
                }

                console.log('term');
                console.log(term);
                pattern = new RegExp(
                    '\\W(' + fullData.metalists[term].map(escapeRegExp).join('|') + ')\\W',
                    'gim'
                );
            }

            for (var i in fullData.docs.extra) {
                if (term in fullData.docs.extra[i]) {
                    var strength = fullData.docs.extra[i][term] /
                        Object.values(fullData.docs.extra[i]).reduce(
                            function (a, b) {
                                return a + b
                            });

                    var docLabel = fullData.docs.labels[i];
                    var numericLabel = -1;
                    if (docLabel == categoryNum) {
                        numericLabel = 0;
                    } else if (notCategoryNumList.indexOf(docLabel) > -1) {
                        numericLabel = 1;
                    } else if (neutralCategoryNumList.indexOf(docLabel) > -1) {
                        numericLabel = 2;
                    } else if (extraCategoryNumList.indexOf(docLabel) > -1) {
                        numericLabel = 3;
                    }
                    if (numericLabel == -1) {
                        continue;
                    }
                    var text = fullData.docs.texts[i];
                    if (!useFullDoc)
                        text = text.slice(0, 300);
                    if (pattern !== null) {
                        text = text.replace(pattern, '<b>$&</b>');
                    }
                    var curMatch = {
                        'id': i,
                        'snippets': [text],
                        'strength': strength,
                        'docLabel': docLabel,
                        'meta': fullData.docs.meta ? fullData.docs.meta[i] : ""
                    }

                    matches[numericLabel].push(curMatch);
                }
            }
            for (var i in [0, 1]) {
                matches[i] = matches[i].sort(function (a, b) {
                    return a.strength < b.strength ? 1 : -1
                })
            }
            return {'contexts': matches, 'info': d};
        }

        // from https://mathiasbynens.be/notes/es-unicode-property-escapes#emoji
        var emojiRE = (/(?:[\u261D\u26F9\u270A-\u270D]|\uD83C[\uDF85\uDFC2-\uDFC4\uDFC7\uDFCA-\uDFCC]|\uD83D[\uDC42\uDC43\uDC46-\uDC50\uDC66-\uDC69\uDC6E\uDC70-\uDC78\uDC7C\uDC81-\uDC83\uDC85-\uDC87\uDCAA\uDD74\uDD75\uDD7A\uDD90\uDD95\uDD96\uDE45-\uDE47\uDE4B-\uDE4F\uDEA3\uDEB4-\uDEB6\uDEC0\uDECC]|\uD83E[\uDD18-\uDD1C\uDD1E\uDD1F\uDD26\uDD30-\uDD39\uDD3D\uDD3E\uDDD1-\uDDDD])(?:\uD83C[\uDFFB-\uDFFF])?|(?:[\u231A\u231B\u23E9-\u23EC\u23F0\u23F3\u25FD\u25FE\u2614\u2615\u2648-\u2653\u267F\u2693\u26A1\u26AA\u26AB\u26BD\u26BE\u26C4\u26C5\u26CE\u26D4\u26EA\u26F2\u26F3\u26F5\u26FA\u26FD\u2705\u270A\u270B\u2728\u274C\u274E\u2753-\u2755\u2757\u2795-\u2797\u27B0\u27BF\u2B1B\u2B1C\u2B50\u2B55]|\uD83C[\uDC04\uDCCF\uDD8E\uDD91-\uDD9A\uDDE6-\uDDFF\uDE01\uDE1A\uDE2F\uDE32-\uDE36\uDE38-\uDE3A\uDE50\uDE51\uDF00-\uDF20\uDF2D-\uDF35\uDF37-\uDF7C\uDF7E-\uDF93\uDFA0-\uDFCA\uDFCF-\uDFD3\uDFE0-\uDFF0\uDFF4\uDFF8-\uDFFF]|\uD83D[\uDC00-\uDC3E\uDC40\uDC42-\uDCFC\uDCFF-\uDD3D\uDD4B-\uDD4E\uDD50-\uDD67\uDD7A\uDD95\uDD96\uDDA4\uDDFB-\uDE4F\uDE80-\uDEC5\uDECC\uDED0-\uDED2\uDEEB\uDEEC\uDEF4-\uDEF8]|\uD83E[\uDD10-\uDD3A\uDD3C-\uDD3E\uDD40-\uDD45\uDD47-\uDD4C\uDD50-\uDD6B\uDD80-\uDD97\uDDC0\uDDD0-\uDDE6])|(?:[#\*0-9\xA9\xAE\u203C\u2049\u2122\u2139\u2194-\u2199\u21A9\u21AA\u231A\u231B\u2328\u23CF\u23E9-\u23F3\u23F8-\u23FA\u24C2\u25AA\u25AB\u25B6\u25C0\u25FB-\u25FE\u2600-\u2604\u260E\u2611\u2614\u2615\u2618\u261D\u2620\u2622\u2623\u2626\u262A\u262E\u262F\u2638-\u263A\u2640\u2642\u2648-\u2653\u2660\u2663\u2665\u2666\u2668\u267B\u267F\u2692-\u2697\u2699\u269B\u269C\u26A0\u26A1\u26AA\u26AB\u26B0\u26B1\u26BD\u26BE\u26C4\u26C5\u26C8\u26CE\u26CF\u26D1\u26D3\u26D4\u26E9\u26EA\u26F0-\u26F5\u26F7-\u26FA\u26FD\u2702\u2705\u2708-\u270D\u270F\u2712\u2714\u2716\u271D\u2721\u2728\u2733\u2734\u2744\u2747\u274C\u274E\u2753-\u2755\u2757\u2763\u2764\u2795-\u2797\u27A1\u27B0\u27BF\u2934\u2935\u2B05-\u2B07\u2B1B\u2B1C\u2B50\u2B55\u3030\u303D\u3297\u3299]|\uD83C[\uDC04\uDCCF\uDD70\uDD71\uDD7E\uDD7F\uDD8E\uDD91-\uDD9A\uDDE6-\uDDFF\uDE01\uDE02\uDE1A\uDE2F\uDE32-\uDE3A\uDE50\uDE51\uDF00-\uDF21\uDF24-\uDF93\uDF96\uDF97\uDF99-\uDF9B\uDF9E-\uDFF0\uDFF3-\uDFF5\uDFF7-\uDFFF]|\uD83D[\uDC00-\uDCFD\uDCFF-\uDD3D\uDD49-\uDD4E\uDD50-\uDD67\uDD6F\uDD70\uDD73-\uDD7A\uDD87\uDD8A-\uDD8D\uDD90\uDD95\uDD96\uDDA4\uDDA5\uDDA8\uDDB1\uDDB2\uDDBC\uDDC2-\uDDC4\uDDD1-\uDDD3\uDDDC-\uDDDE\uDDE1\uDDE3\uDDE8\uDDEF\uDDF3\uDDFA-\uDE4F\uDE80-\uDEC5\uDECB-\uDED2\uDEE0-\uDEE5\uDEE9\uDEEB\uDEEC\uDEF0\uDEF3-\uDEF8]|\uD83E[\uDD10-\uDD3A\uDD3C-\uDD3E\uDD40-\uDD45\uDD47-\uDD4C\uDD50-\uDD6B\uDD80-\uDD97\uDDC0\uDDD0-\uDDE6])\uFE0F/g);

        function isEmoji(str) {
            if (str.match(emojiRE)) return true;
            return false;
        }

        function displayObscuredTerms(obscuredTerms, data, term, termInfo, div = '#' + divName + '-' + 'overlapped-terms') {
            d3.select('#' + divName + '-' + 'overlapped-terms')
                .selectAll('div')
                .remove();
            d3.select(div)
                .selectAll('div')
                .remove();
            if (obscuredTerms.length > 1 && maxOverlapping !== 0) {
                var obscuredDiv = d3.select(div)
                    .append('div')
                    .attr("class", "obscured")
                    .style('align', 'center')
                    .style('text-align', 'center')
                    .html("<b>\"" + term + "\" obstructs</b>: ");
                obscuredTerms.map(
                    function (term, i) {
                        if (maxOverlapping === -1 || i < maxOverlapping) {
                            makeWordInteractive(
                                data,
                                svg,
                                obscuredDiv.append("text").text(term),
                                term,
                                data.filter(t => t.term === term)[0],//termInfo
                                false
                            );
                            if (i < obscuredTerms.length - 1
                                && (maxOverlapping === -1 || i < maxOverlapping - 1)) {
                                obscuredDiv.append("text").text(", ");
                            }
                        } else if (i === maxOverlapping && i !== obscuredTerms.length - 1) {
                            obscuredDiv.append("text").text("...");
                        }
                    }
                )
            }
        }

        function displayTermContexts(data, termInfo, jump = true, includeAll = false) {
            var contexts = termInfo.contexts;
            var info = termInfo.info;
            var notmatches = termInfo.notmatches;
            if (contexts[0].length + contexts[1].length + contexts[2].length + contexts[3].length == 0) {
                //return null;
            }
            //!!! Future feature: context words
            //var contextWords = getContextWordSFS(info.term);
            //var contextWords = getContextWordLORIPs(info.term);
            //var categoryNames = [fullData.info.category_name,
            //    fullData.info.not_category_name];
            var catInternalName = fullData.info.category_internal_name;


            function addSnippets(contexts, divId, isMatch = true) {
                var meta = contexts.meta ? contexts.meta : '&nbsp;';
                var headClass = 'snippet_meta docLabel' + contexts.docLabel;
                var snippetClass = 'snippet docLabel' + contexts.docLabel;
                if (!isMatch) {
                    headClass = 'snippet_meta not_match docLabel' + contexts.docLabel;
                    snippetClass = 'snippet not_match docLabel' + contexts.docLabel;
                }
                d3.select(divId)
                    .append("div")
                    .attr('class', headClass)
                    .html(meta);
                contexts.snippets.forEach(function (snippet) {
                    d3.select(divId)
                        .append("div")
                        .attr('class', snippetClass)
                        .html(snippet);
                })
            }

            if (unifiedContexts) {
                divId = '#' + divName + '-' + 'cat';
                var docLabelCounts = fullData.docs.labels.reduce(
                    function (map, label) {
                        map[label] = (map[label] || 0) + 1;
                        return map;
                    },
                    Object.create(null)
                );
                var numMatches = Object.create(null);
                var temp = d3.select(divId).selectAll("div").remove();
                var allContexts = contexts[0].concat(contexts[1]).concat(contexts[2]).concat(contexts[3]);
                allContexts.forEach(function (singleDoc) {
                    numMatches[singleDoc.docLabel] = (numMatches[singleDoc.docLabel] || 0) + 1;
                });
                var allNotMatches = notmatches[0].concat(notmatches[1]).concat(notmatches[2]).concat(notmatches[3]);

                /*contexts.forEach(function(context) {
                     context.forEach(function (singleDoc) {
                         numMatches[singleDoc.docLabel] = (numMatches[singleDoc.docLabel]||0) + 1;
                         addSnippets(singleDoc, divId);
                     });
                 });*/
                var docLabelCountsSorted = Object.keys(docLabelCounts).map(key => (
                    {
                        "label": fullData.docs.categories[key],
                        "labelNum": key,
                        "matches": numMatches[key] || 0,
                        "overall": docLabelCounts[key],
                        'percent': (numMatches[key] || 0) * 100. / docLabelCounts[key]
                    }))
                    .sort(function (a, b) {
                        if (sortDocLabelsByName) {
                            return a['label'] < b['label'] ? 1 : a['label'] > b['label'] ? -1 : 0;
                        } else {
                            return b.percent - a.percent;
                        }
                    });
                console.log("docLabelCountsSorted")
                console.log(docLabelCountsSorted);
                console.log(numMatches)
                console.log('#' + divName + '-' + 'categoryinfo')
                d3.select('#' + divName + '-' + 'categoryinfo').selectAll("div").remove();
                if (showCategoryHeadings) {
                    d3.select('#' + divName + '-' + 'categoryinfo').attr('display', 'inline');
                }

                function getCategoryStatsHTML(counts) {
                    return counts.matches + " document"
                        + (counts.matches == 1 ? "" : "s") + " out of " + counts.overall + ': '
                        + counts['percent'].toFixed(2) + '%';
                }

                function getCategoryInlineHeadingHTML(counts) {
                    return '<a name="' + divName + '-category'
                        + counts.labelNum + '"></a>'
                        + counts.label + ": <span class=topic_preview>"
                        + getCategoryStatsHTML(counts)
                        + "</span>";
                }


                docLabelCountsSorted.forEach(function (counts) {
                    var htmlToAdd = "<b>" + counts.label + "</b>: " + getCategoryStatsHTML(counts);

                    if (counts.matches > 0) {
                        d3.select(divId)
                            .append("div")
                            .attr('class', 'text_header')
                            .html(getCategoryInlineHeadingHTML(counts));
                        allContexts
                            .filter(singleDoc => singleDoc.docLabel == counts.labelNum)
                            .forEach(function (singleDoc) {
                                addSnippets(singleDoc, divId);
                            });
                        if (includeAll) {
                            allNotMatches
                                .filter(singleDoc => singleDoc.docLabel == counts.labelNum)
                                .forEach(function (singleDoc) {
                                    addSnippets(singleDoc, divId, false);
                                });
                        }
                    }


                    if (showCategoryHeadings) {
                        d3.select('#' + divName + '-' + 'categoryinfo')
                            .attr('display', 'inline')
                            .append('div')
                            .html(htmlToAdd)
                            .on("click", function () {
                                window.location.hash = '#' + divName + '-' + 'category' + counts.labelNum
                            });
                    }

                })


            } else {
                var contextColumns = [
                    fullData.info.category_internal_name,
                    fullData.info.not_category_name
                ];
                if (showNeutral) {
                    if ('neutral_category_name' in fullData.info) {
                        contextColumns.push(fullData.info.neutral_category_name)
                    } else {
                        contextColumns.push("Neutral")
                    }
                    if (showExtra) {
                        if ('extra_category_name' in fullData.info) {
                            contextColumns.push(fullData.info.extra_category_name)
                        } else {
                            contextColumns.push("Extra")
                        }
                    }

                }
                contextColumns.map(
                    function (catName, catIndex) {
                        if (max_snippets != null) {
                            var contextsToDisplay = contexts[catIndex].slice(0, max_snippets);
                        }
                        console.log("CATCAT")
                        console.log(catName, catIndex)
                        //var divId = catName == catInternalName ? '#cat' : '#notcat';
                        var divId = null
                        if (fullData.info.category_internal_name == catName) {
                            divId = '#' + divName + '-' + 'cat'
                        } else if (fullData.info.not_category_name == catName) {
                            divId = '#' + divName + '-' + 'notcat'
                        } else if (fullData.info.neutral_category_name == catName) {
                            divId = '#' + divName + '-' + 'neut';
                        } else if (fullData.info.extra_category_name == catName) {
                            divId = '#' + divName + '-' + 'extra'
                        } else {
                            return;
                        }
                        console.log('divid');
                        console.log(divId)

                        var temp = d3.select(divId).selectAll("div").remove();
                        contexts[catIndex].forEach(function (context) {
                            addSnippets(context, divId);
                        });
                        if (includeAll) {
                            notmatches[catIndex].forEach(function (context) {
                                addSnippets(context, divId, false);
                            });
                        }
                    }
                );
            }

            var obscuredTerms = getObscuredTerms(data, termInfo.info);
            displayObscuredTerms(obscuredTerms, data, info.term, info, '#' + divName + '-' + 'overlapped-terms-clicked');

            d3.select('#' + divName + '-' + 'termstats')
                .selectAll("div")
                .remove();
            var termHtml = 'Term: <b>' + info.term + '</b>';
            if ('metalists' in fullData && info.term in fullData.metalists) {
                termHtml = 'Topic: <b>' + info.term + '</b>';
            }
            d3.select('#' + divName + '-' + 'termstats')
                .append('div')
                .attr("class", "snippet_header")
                .html(termHtml);
            if ('metalists' in fullData && info.term in fullData.metalists && topic_model_preview_size > 0) {
                d3.select('#' + divName + '-' + 'termstats')
                    .attr("class", "topic_preview")
                    .append('div')
                    .html("<b>Topic preview</b>: "
                        + fullData.metalists[info.term]
                            .slice(0, topic_model_preview_size)
                            .reduce(function (x, y) {
                                return x + ', ' + y
                            }));
            }
            if ('metadescriptions' in fullData && info.term in fullData.metadescriptions) {
                d3.select('#' + divName + '-' + 'termstats')
                    .attr("class", "topic_preview")
                    .append('div')
                    .html("<b>Description</b>: " + fullData.metadescriptions[info.term]);
            }
            var message = '';
            var cat_name = fullData.info.category_name;
            var ncat_name = fullData.info.not_category_name;


            var numCatDocs = fullData.docs.labels
                .map(function (x) {
                    return (x == fullData.docs.categories.indexOf(
                        fullData.info.category_internal_name)) + 0
                })
                .reduce(function (a, b) {
                    return a + b;
                }, 0);

            var notCategoryNumList = fullData.docs.categories.map(function (x, i) {
                if (fullData.info.not_category_internal_names.indexOf(x) > -1) {
                    return i;
                } else {
                    return -1;
                }
            }).filter(function (x) {
                return x > -1
            });


            var numNCatDocs = fullData.docs.labels
                .map(function (x) {
                    return notCategoryNumList.indexOf(x) > -1
                })
                .reduce(function (a, b) {
                    return a + b;
                }, 0);

            function getFrequencyDescription(name, count25k, count, ndocs) {
                var desc = name + ' frequency: <div class=text_subhead>' + count25k + ' per 25,000 terms</div>';
                if (!isNaN(Math.round(ndocs))) {
                    desc += '<div class=text_subhead>' + Math.round(ndocs) + ' per 1,000 docs</div>';
                }
                if (count == 0) {
                    desc += '<u>Not found in any ' + name + ' documents.</u>';
                } else {
                    if (!isNaN(Math.round(ndocs))) {
                        desc += '<u>Some of the ' + count + ' mentions:</u>';
                    } else {
                        desc += count + ' mentions';
                    }
                }
                /*
                desc += '<br><b>Discriminative:</b> ';

                desc += contextWords
                    .slice(cat_name === name ? 0 : contextWords.length - 3,
                        cat_name === name ? 3 : contextWords.length)
                    .filter(function (x) {
                        //return Math.abs(x[5]) > 1.96;
                        return true;
                    })
                    .map(function (x) {return x.join(', ')}).join('<br>');
                */
                return desc;
            }

            if (!unifiedContexts) {
                console.log("NOT UNIFIED CONTEXTS")
                d3.select('#' + divName + '-' + 'cathead')
                    .style('fill', color(1))
                    .html(
                        getFrequencyDescription(cat_name,
                            info.cat25k,
                            info.cat,
                            termInfo.contexts[0].length * 1000 / numCatDocs
                        )
                    );
                d3.select('#' + divName + '-' + 'notcathead')
                    .style('fill', color(0))
                    .html(
                        getFrequencyDescription(ncat_name,
                            info.ncat25k,
                            info.ncat,
                            termInfo.contexts[1].length * 1000 / numNCatDocs)
                    );
                console.log("TermINfo")
                console.log(termInfo);
                console.log(info)
                if (showNeutral) {
                    console.log("NEUTRAL")

                    var numList = fullData.docs.categories.map(function (x, i) {
                        if (fullData.info.neutral_category_internal_names.indexOf(x) > -1) {
                            return i;
                        } else {
                            return -1;
                        }
                    }).filter(function (x) {
                        return x > -1
                    });

                    var numDocs = fullData.docs.labels
                        .map(function (x) {
                            return numList.indexOf(x) > -1
                        })
                        .reduce(function (a, b) {
                            return a + b;
                        }, 0);

                    d3.select("#" + divName + "-neuthead")
                        .style('fill', color(0))
                        .html(
                            getFrequencyDescription(fullData.info.neutral_category_name,
                                info.neut25k,
                                info.neut,
                                termInfo.contexts[2].length * 1000 / numDocs)
                        );

                    if (showExtra) {
                        console.log("EXTRA")
                        var numList = fullData.docs.categories.map(function (x, i) {
                            if (fullData.info.extra_category_internal_names.indexOf(x) > -1) {
                                return i;
                            } else {
                                return -1;
                            }
                        }).filter(function (x) {
                            return x > -1
                        });

                        var numDocs = fullData.docs.labels
                            .map(function (x) {
                                return numList.indexOf(x) > -1
                            })
                            .reduce(function (a, b) {
                                return a + b;
                            }, 0);

                        d3.select("#" + divName + "-extrahead")
                            .style('fill', color(0))
                            .html(
                                getFrequencyDescription(fullData.info.extra_category_name,
                                    info.extra25k,
                                    info.extra,
                                    termInfo.contexts[3].length * 1000 / numDocs)
                            );

                    }
                }
            } else {
                // extra unified context code goes here
                console.log("docLabelCountsSorted")
                console.log(docLabelCountsSorted)

                docLabelCountsSorted.forEach(function (counts) {
                    var htmlToAdd = "<b>" + counts.label + "</b>: " + getCategoryStatsHTML(counts);
                    if (showCategoryHeadings) {
                        console.log("XXXX")
                        d3.select('#' + divName + '-' + 'contexts')
                            .append('div')
                            .html("XX" + htmlToAdd)
                            .on("click", function () {
                                window.location.hash = '#' + divName + '-' + 'category' + counts.labelNum
                            });
                    }
                })
            }
            if (jump) {
                if (window.location.hash == '#' + divName + '-' + 'snippets') {
                    window.location.hash = '#' + divName + '-' + 'snippetsalt';
                } else {
                    window.location.hash = '#' + divName + '-' + 'snippets';
                }
            }
        }

        function searchInText(d, includeAll = true) {
            function stripNonWordChars(term) {
                //d.term.replace(" ", "[^\\w]+")
            }

            function removeUnderScoreJoin(term) {
                /*
                '_ _asjdklf_jaksdlf_jaksdfl skld_Jjskld asdfjkl_sjkdlf'
                  ->
                "_ _asjdklf jaksdlf jaksdfl skld Jjskld asdfjkl_sjkdlf"
                 */
                return term.replace(/(\w+)(_)(\w+)/, "$1 $3")
                    .replace(/(\w+)(_)(\w+)/, "$1 $3")
                    .replace(/(\w+)(_)(\w+)/, "$1 $3");
            }

            function buildMatcher(term) {

                var boundary = '(?:\\W|^|$)';
                var wordSep = "[^\\w]+";
                if (asianMode) {
                    boundary = '( |$|^)';
                    wordSep = ' ';
                }
                if (isEmoji(term)) {
                    boundary = '';
                    wordSep = '';
                }
                if (matchFullLine) {
                    boundary = '($|^)';
                }
                var termToRegex = term;

                // https://stackoverflow.com/questions/3446170/escape-string-for-use-in-javascript-regex
                function escapeRegExp(string) {
                    return string.replace(/[#.*+?^${}()|[\]\\]/g, '\\$&'); // $& means the whole matched string
                }

                /*
                ['[', ']', '(', ')', '{', '}', '^', '$', '|', '?', '"',
                    '*', '+', '-', '=', '~', '`', '{'].forEach(function (a) {
                    termToRegex = termToRegex.replace(a, '\\\\' + a)
                });
                ['.', '#'].forEach(function(a) {termToRegex = termToRegex.replace(a, '\\' + a)})
                */
                termToRegex = escapeRegExp(termToRegex);
                console.log("termToRegex")
                console.log(termToRegex)
                var regexp = new RegExp(boundary + '('
                    + removeUnderScoreJoin(
                        termToRegex.replace(' ', wordSep, 'gim')
                    )
                    + ')' + boundary, 'gim');
                console.log(regexp);
                try {
                    regexp.exec('X');
                } catch (err) {
                    console.log("Can't search " + term);
                    console.log(err);
                    return null;
                }
                return regexp;
            }

            var matches = [[], [], [], []];
            var notmatches = [[], [], [], []];
            var pattern = buildMatcher(d.term);
            var categoryNum = fullData.docs.categories.indexOf(fullData.info.category_internal_name);
            var notCategoryNumList = fullData.docs.categories.map(function (x, i) {
                if (fullData.info.not_category_internal_names.indexOf(x) > -1) {
                    return i;
                } else {
                    return -1;
                }
            }).filter(function (x) {
                return x > -1
            });
            var neutralCategoryNumList = fullData.docs.categories.map(function (x, i) {
                if (fullData.info.neutral_category_internal_names.indexOf(x) > -1) {
                    return i;
                } else {
                    return -1;
                }
            }).filter(function (x) {
                return x > -1
            });
            var extraCategoryNumList = fullData.docs.categories.map(function (x, i) {
                if (fullData.info.extra_category_internal_names.indexOf(x) > -1) {
                    return i;
                } else {
                    return -1;
                }
            }).filter(function (x) {
                return x > -1
            });
            console.log('extraCategoryNumList')
            console.log(extraCategoryNumList);
            console.log("categoryNum");
            console.log(categoryNum);
            console.log("categoryNum");
            if (pattern !== null) {
                for (var i in fullData.docs.texts) {
                    //var numericLabel = 1 * (fullData.docs.categories[fullData.docs.labels[i]] != fullData.info.category_internal_name);

                    var docLabel = fullData.docs.labels[i];
                    var numericLabel = -1;
                    if (docLabel == categoryNum) {
                        numericLabel = 0;
                    } else if (notCategoryNumList.indexOf(docLabel) > -1) {
                        numericLabel = 1;
                    } else if (neutralCategoryNumList.indexOf(docLabel) > -1) {
                        numericLabel = 2;
                    } else if (extraCategoryNumList.indexOf(docLabel) > -1) {
                        numericLabel = 3;
                    }
                    if (numericLabel == -1) {
                        continue;
                    }

                    var text = removeUnderScoreJoin(fullData.docs.texts[i]);
                    //var pattern = new RegExp("\\b(" + stripNonWordChars(d.term) + ")\\b", "gim");
                    var match;
                    var sentenceOffsets = null;
                    var lastSentenceStart = null;
                    var matchFound = false;
                    var curMatch = {'id': i, 'snippets': [], 'notsnippets': [], 'docLabel': docLabel};
                    if (fullData.docs.meta) {
                        curMatch['meta'] = fullData.docs.meta[i];
                    }

                    while ((match = pattern.exec(text)) != null) {
                        if (sentenceOffsets == null) {
                            sentenceOffsets = getSentenceBoundaries(text);
                        }
                        var foundSnippet = getMatchingSnippet(text, sentenceOffsets,
                            match.index, pattern.lastIndex);
                        if (foundSnippet.sentenceStart == lastSentenceStart) continue; // ensure we don't duplicate sentences
                        lastSentenceStart = foundSnippet.sentenceStart;
                        curMatch.snippets.push(foundSnippet.snippet);
                        matchFound = true;
                    }
                    if (matchFound) {
                        if (useFullDoc) {
                            curMatch.snippets = [
                                text
                                    .replace(/\n$/g, '\n\n')
                                    .replace(
                                        //new RegExp("\\b(" + d.term.replace(" ", "[^\\w]+") + ")\\b",
                                        //    'gim'),
                                        pattern,
                                        '<b>$&</b>')
                            ];
                        }
                        matches[numericLabel].push(curMatch);
                    } else {
                        if (includeAll) {
                            curMatch.snippets = [
                                text.replace(/\n$/g, '\n\n')
                            ];
                            notmatches[numericLabel].push(curMatch);
                        }

                    }
                }
            }
            var toRet = {
                'contexts': matches,
                'notmatches': notmatches,
                'info': d,
                'docLabel': docLabel
            };
            return toRet;
        }

        function getDefaultTooltipContent(d) {
            var message = d.term + "<br/>" + d.cat25k + ":" + d.ncat25k + " per 25k words";
            message += '<br/>score: ' + d.os.toFixed(5);
            return message;
        }

        function getDefaultTooltipContentWithoutScore(d) {
            var message = d.term + "<br/>" + d.cat25k + ":" + d.ncat25k + " per 25k words";
            return message;
        }

        function getObscuredTerms(data, d) {
            //data = fullData['data']
            var matches = (data.filter(function (term) {
                    return term.x === d.x && term.y === d.y && (term.display === undefined || term.display === true);
                }).map(function (term) {
                    return term.term
                }).sort()
            );
            return matches;
        }

        function showTooltip(data, d, pageX, pageY, showObscured = true) {
            deselectLastCircle();

            var obscuredTerms = getObscuredTerms(data, d);
            var message = '';
            console.log("!!!!! " + obscuredTerms.length)
            console.log(showObscured)
            if (obscuredTerms.length > 1 && showObscured)
                displayObscuredTerms(obscuredTerms, data, d.term, d);
            if (getTooltipContent !== null) {
                message += getTooltipContent(d);
            } else {
                if (sortByDist) {
                    message += getDefaultTooltipContentWithoutScore(d);
                } else {
                    message += getDefaultTooltipContent(d);
                }
            }
            pageX -= (svg.node().getBoundingClientRect().left) - origSVGLeft;
            pageY -= (svg.node().getBoundingClientRect().top) - origSVGTop;
            tooltip.transition()
                .duration(0)
                .style("opacity", 1)
                .style("z-index", 10000000);
            tooltip.html(message)
                .style("left", (pageX - 40) + "px")
                .style("top", (pageY - 85 > 0 ? pageY - 85 : 0) + "px");
            tooltip.on('click', function () {
                tooltip.transition()
                    .style('opacity', 0)
            }).on('mouseout', function () {
                tooltip.transition().style('opacity', 0)
            });
        }

        handleSearch = function (event) {
            var searchTerm = document
                .getElementById(this.divName + "-searchTerm")
                .value;
            handleSearchTerm(searchTerm);
            return false;
        };

        function highlightTerm(searchTerm, showObscured) {
            deselectLastCircle();
            var cleanedTerm = searchTerm.toLowerCase()
                .replace("'", " '")
                .trim();
            if (this.termDict[cleanedTerm] === undefined) {
                cleanedTerm = searchTerm.replace("'", " '").trim();
            }
            if (this.termDict[cleanedTerm] !== undefined) {
                showToolTipForTerm(this.data, this.svg, cleanedTerm, this.termDict[cleanedTerm], showObscured);
            }
            return cleanedTerm;
        }

        function handleSearchTerm(searchTerm, jump = false) {
            console.log("Handle search term.");
            console.log(searchTerm);
            console.log("this");
            console.log(this)
            highlighted = highlightTerm.call(this, searchTerm, true);
            console.log("found searchTerm");
            console.log(searchTerm);
            if (this.termDict[searchTerm] != null) {
                var runDisplayTermContexts = true;
                if (alternativeTermFunc != null) {
                    runDisplayTermContexts = this.alternativeTermFunc(this.termDict[searchTerm]);
                }
                if (runDisplayTermContexts) {
                    displayTermContexts(
                        this.data,
                        this.gatherTermContexts(this.termDict[searchTerm], this.includeAllContexts),
                        jump,
                        this.includeAllContexts
                    );
                }
            }
        }

        function showToolTipForTerm(data, mysvg, searchTerm, searchTermInfo, showObscured = true) {
            //var searchTermInfo = termDict[searchTerm];
            console.log("showing tool tip")
            console.log(searchTerm)
            console.log(searchTermInfo)
            if (searchTermInfo === undefined) {
                console.log("can't show")
                d3.select("#" + divName + "-alertMessage")
                    .text(searchTerm + " didn't make it into the visualization.");
            } else {
                d3.select("#" + divName + "-alertMessage").text("");
                var circle = mysvg;
                console.log("mysvg");
                console.log(mysvg)
                if (circle.tagName !== "circle") { // need to clean this thing up
                    circle = mysvg._groups[0][searchTermInfo.ci];
                    if (circle === undefined || circle.tagName != 'circle') {
                        console.log("circle0")
                        if (mysvg._groups[0].children !== undefined) {
                            circle = mysvg._groups[0].children[searchTermInfo.ci];
                        }
                    }
                    if (circle === undefined || circle.tagName != 'circle') {
                        console.log("circle1");
                        if (mysvg._groups[0][0].children !== undefined) {
                            circle = Array.prototype.filter.call(
                                mysvg._groups[0][0].children,
                                x => (x.tagName == "circle" && x.__data__['term'] == searchTermInfo.term)
                            )[0];
                        }
                        console.log(circle)
                    }
                    if ((circle === undefined || circle.tagName != 'circle') && mysvg._groups[0][0].children !== undefined) {
                        console.log("circle2");
                        console.log(mysvg._groups[0][0])
                        console.log(mysvg._groups[0][0].children)
                        console.log(searchTermInfo.ci);
                        circle = mysvg._groups[0][0].children[searchTermInfo.ci];
                        console.log(circle)
                    }
                }
                if (circle) {
                    var mySVGMatrix = circle.getScreenCTM().translate(circle.cx.baseVal.value, circle.cy.baseVal.value);
                    var pageX = mySVGMatrix.e;
                    var pageY = mySVGMatrix.f;
                    circle.style["stroke"] = "black";
                    //var circlePos = circle.position();
                    //var el = circle.node()
                    //showTooltip(searchTermInfo, pageX, pageY, circle.cx.baseVal.value, circle.cx.baseVal.value);
                    showTooltip(
                        data,
                        searchTermInfo,
                        pageX,
                        pageY,
                        showObscured
                    );

                    lastCircleSelected = circle;
                }

            }
        };


        function makeWordInteractive(data, svg, domObj, term, termInfo, showObscured = true) {
            return domObj
                .on("mouseover", function (d) {
                    console.log("mouseover")
                    console.log(term)
                    console.log(termInfo)
                    showToolTipForTerm(data, svg, term, termInfo, showObscured);
                    d3.select(this).style("stroke", "black");
                })
                .on("mouseout", function (d) {
                    tooltip.transition()
                        .duration(0)
                        .style("opacity", 0);
                    d3.select(this).style("stroke", null);
                    if (showObscured) {
                        d3.select('#' + divName + '-' + 'overlapped-terms')
                            .selectAll('div')
                            .remove();
                    }
                })
                .on("click", function (d) {
                    var runDisplayTermContexts = true;
                    if (alternativeTermFunc != null) {
                        runDisplayTermContexts = alternativeTermFunc(termInfo);
                    }
                    if (runDisplayTermContexts) {
                        displayTermContexts(data, gatherTermContexts(termInfo, includeAllContexts), true, includeAllContexts);
                    }
                });
        }

        function processData(fullData) {

            modelInfo = fullData['info'];
            /*
             categoryTermList.data(modelInfo['category_terms'])
             .enter()
             .append("li")
             .text(function(d) {return d;});
             */
            var data = fullData['data'];
            termDict = Object();
            data.forEach(function (x, i) {
                termDict[x.term] = x;
                //!!!
                //termDict[x.term].i = i;
            });

            var padding = 0;
            if (showAxes || showAxesAndCrossHairs) {
                padding = 0.1;
            }

            // Scale the range of the data.  Add some space on either end.
            x.domain([-1 * padding, d3.max(data, function (d) {
                return d.x;
            }) + padding]);
            y.domain([-1 * padding, d3.max(data, function (d) {
                return d.y;
            }) + padding]);

            /*
             data.sort(function (a, b) {
             return Math.abs(b.os) - Math.abs(a.os)
             });
             */


            //var rangeTree = null; // keep boxes of all points and labels here
            var rectHolder = new RectangleHolder();
            // Add the scatterplot
            data.forEach(function (d, i) {
                d.ci = i
            });
            //console.log('XXXXX'); console.log(data)
            var mysvg = svg
                .selectAll("dot")
                .data(data.filter(d => d.display === undefined || d.display === true))
                //.filter(function (d) {return d.display === undefined || d.display === true})
                .enter()
                .append("circle")
                .attr("r", function (d) {
                    if (pValueColors && d.p) {
                        return (d.p >= 1 - minPVal || d.p <= minPVal) ? 2 : 1.75;
                    }
                    return 2;
                })
                .attr("cx", function (d) {
                    return x(d.x);
                })
                .attr("cy", function (d) {
                    return y(d.y);
                })
                .style("fill", function (d) {
                    //.attr("fill", function (d) {
                    if (colorFunc) {
                        return colorFunc(d);
                    } else if (greyZeroScores && d.os == 0) {
                        return d3.rgb(230, 230, 230);
                    } else if (pValueColors && d.p) {
                        if (d.p >= 1 - minPVal) {
                            return wordVecMaxPValue ? d3.interpolateYlGnBu(d.s) : color(d.s);
                        } else if (d.p <= minPVal) {
                            return wordVecMaxPValue ? d3.interpolateYlGnBu(d.s) : color(d.s);
                        } else {
                            return interpolateLightGreys(d.s);
                        }
                    } else {
                        if (d.term == "psychological") {
                            console.log("COLS " + d.s + " " + color(d.s) + " " + d.term)
                            console.log(d)
                            console.log(color)
                        }
                        return color(d.s);
                    }
                })
                .on("mouseover", function (d) {
                    /*var mySVGMatrix = circle.getScreenCTM()n
                        .translate(circle.cx.baseVal.value, circle.cy.baseVal.value);
                    var pageX = mySVGMatrix.e;
                    var pageY = mySVGMatrix.f;*/

                    /*showTooltip(
                        d,
                        d3.event.pageX,
                        d3.event.pageY
                    );*/
                    console.log("point MOUSOEVER")
                    console.log(d)
                    showToolTipForTerm(data, this, d.term, d, true);
                    d3.select(this).style("stroke", "black");
                })
                .on("click", function (d) {
                    var runDisplayTermContexts = true;
                    if (alternativeTermFunc != null) {
                        runDisplayTermContexts = alternativeTermFunc(d);
                    }
                    if (runDisplayTermContexts) {
                        displayTermContexts(data, gatherTermContexts(d), true, includeAllContexts);
                    }
                })
                .on("mouseout", function (d) {
                    tooltip.transition()
                        .duration(0)
                        .style("opacity", 0);
                    d3.select(this).style("stroke", null);
                    d3.select('#' + divName + '-' + 'overlapped-terms')
                        .selectAll('div')
                        .remove();
                })


            coords = Object();

            var pointStore = [];
            var pointRects = [];

            function censorPoints(datum, getX, getY) {
                var term = datum.term;
                var curLabel = svg.append("text")
                    .attr("x", x(getX(datum)))
                    .attr("y", y(getY(datum)) + 3)
                    .attr("text-anchor", "middle")
                    .text("x");
                var bbox = curLabel.node().getBBox();
                var borderToRemove = .5;
                var x1 = bbox.x + borderToRemove,
                    y1 = bbox.y + borderToRemove,
                    x2 = bbox.x + bbox.width - borderToRemove,
                    y2 = bbox.y + bbox.height - borderToRemove;
                //rangeTree = insertRangeTree(rangeTree, x1, y1, x2, y2, '~~' + term);
                var pointRect = new Rectangle(x1, y1, x2, y2);
                pointRects.push(pointRect);
                rectHolder.add(pointRect);
                pointStore.push([x1, y1]);
                pointStore.push([x2, y1]);
                pointStore.push([x1, y2]);
                pointStore.push([x2, y2]);
                curLabel.remove();
            }

            function censorCircle(xCoord, yCoord) {
                var curLabel = svg.append("text")
                    .attr("x", x(xCoord))
                    .attr("y", y(yCoord) + 3)
                    .attr("text-anchor", "middle")
                    .text("x");
                var bbox = curLabel.node().getBBox();
                var borderToRemove = .5;
                var x1 = bbox.x + borderToRemove,
                    y1 = bbox.y + borderToRemove,
                    x2 = bbox.x + bbox.width - borderToRemove,
                    y2 = bbox.y + bbox.height - borderToRemove;
                var pointRect = new Rectangle(x1, y1, x2, y2);
                pointRects.push(pointRect);
                rectHolder.add(pointRect);
                pointStore.push([x1, y1]);
                pointStore.push([x2, y1]);
                pointStore.push([x1, y2]);
                pointStore.push([x2, y2]);
                curLabel.remove();
            }

            function labelPointsIfPossible(datum, myX, myY) {
                var term = datum.term;
                if (term == "the")
                    console.log("TERM " + term + " " + myX + " " + myY)
                //console.log('xxx'); console.log(term); console.log(term.display !== undefined && term.display === false)
                //if(term.display !== undefined && term.display === false) {
                //    return false;
                //}
                var configs = [
                    {'anchor': 'end', 'xoff': -5, 'yoff': -3, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'end', 'xoff': -5, 'yoff': 10, 'alignment-baseline': 'ideographic'},

                    {'anchor': 'end', 'xoff': 10, 'yoff': 15, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'end', 'xoff': -10, 'yoff': -15, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'end', 'xoff': 10, 'yoff': -15, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'end', 'xoff': -10, 'yoff': 15, 'alignment-baseline': 'ideographic'},

                    {'anchor': 'start', 'xoff': 3, 'yoff': 10, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'start', 'xoff': 3, 'yoff': -3, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'start', 'xoff': 5, 'yoff': 10, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'start', 'xoff': 5, 'yoff': -3, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'start', 'xoff': 10, 'yoff': 15, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'start', 'xoff': -10, 'yoff': -15, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'start', 'xoff': 10, 'yoff': -15, 'alignment-baseline': 'ideographic'},
                    {'anchor': 'start', 'xoff': -10, 'yoff': 15, 'alignment-baseline': 'ideographic'},
                ];
                if (centerLabelsOverPoints) {
                    configs = [{'anchor': 'middle', 'xoff': 0, 'yoff': 0, 'alignment-baseline': 'middle'}];
                }
                var matchedElement = null;
                for (var configI in configs) {
                    var config = configs[configI];
                    var curLabel = svg.append("text")
                    //.attr("x", x(data[i].x) + config['xoff'])
                    //.attr("y", y(data[i].y) + config['yoff'])
                        .attr("x", x(myX) + config['xoff'])
                        .attr("y", y(myY) + config['yoff'])
                        .attr('class', 'label')
                        .attr('class', 'pointlabel')
                        .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                        .attr('font-size', '10px')
                        .attr("text-anchor", config['anchor'])
                        .attr("alignment-baseline", config['alignment'])
                        .text(term);
                    var bbox = curLabel.node().getBBox();
                    var borderToRemove = .25;
                    if (doCensorPoints) {
                        var borderToRemove = .5;
                    }

                    var x1 = bbox.x + borderToRemove,
                        y1 = bbox.y + borderToRemove,
                        x2 = bbox.x + bbox.width - borderToRemove,
                        y2 = bbox.y + bbox.height - borderToRemove;
                    //matchedElement = searchRangeTree(rangeTree, x1, y1, x2, y2);
                    var matchedElement = false;
                    rectHolder.findMatchingRectangles(x1, y1, x2, y2, function (elem) {
                        matchedElement = true;
                        return false;
                    });
                    if (matchedElement) {
                        curLabel.remove();
                    } else {
                        curLabel = makeWordInteractive(data, svg, curLabel, term, datum);
                        break;
                    }
                }

                if (!matchedElement) {
                    coords[term] = [x1, y1, x2, y2];
                    //rangeTree = insertRangeTree(rangeTree, x1, y1, x2, y2, term);
                    var labelRect = new Rectangle(x1, y1, x2, y2)
                    rectHolder.add(labelRect);
                    pointStore.push([x1, y1]);
                    pointStore.push([x2, y1]);
                    pointStore.push([x1, y2]);
                    pointStore.push([x2, y2]);
                    return {label: curLabel, rect: labelRect};
                } else {
                    //curLabel.remove();
                    return false;
                }

            }

            var radius = 2;

            function euclideanDistanceSort(a, b) {
                var aCatDist = a.x * a.x + (1 - a.y) * (1 - a.y);
                var aNotCatDist = a.y * a.y + (1 - a.x) * (1 - a.x);
                var bCatDist = b.x * b.x + (1 - b.y) * (1 - b.y);
                var bNotCatDist = b.y * b.y + (1 - b.x) * (1 - b.x);
                return (Math.min(aCatDist, aNotCatDist) > Math.min(bCatDist, bNotCatDist)) * 2 - 1;
            }

            function euclideanDistanceSortForCategory(a, b) {
                var aCatDist = a.x * a.x + (1 - a.y) * (1 - a.y);
                var bCatDist = b.x * b.x + (1 - b.y) * (1 - b.y);
                return (aCatDist > bCatDist) * 2 - 1;
            }

            function euclideanDistanceSortForNotCategory(a, b) {
                var aNotCatDist = a.y * a.y + (1 - a.x) * (1 - a.x);
                var bNotCatDist = b.y * b.y + (1 - b.x) * (1 - b.x);
                return (aNotCatDist > bNotCatDist) * 2 - 1;
            }

            function scoreSort(a, b) {
                return a.s - b.s;
            }

            function scoreSortReverse(a, b) {
                return b.s - a.s;
            }

            function backgroundScoreSort(a, b) {
                if (b.bg === a.bg)
                    return (b.cat + b.ncat) - (a.cat + a.ncat);
                return b.bg - a.bg;
            }

            function arePointsPredictiveOfDifferentCategories(a, b) {
                var aCatDist = a.x * a.x + (1 - a.y) * (1 - a.y);
                var bCatDist = b.x * b.x + (1 - b.y) * (1 - b.y);
                var aNotCatDist = a.y * a.y + (1 - a.x) * (1 - a.x);
                var bNotCatDist = b.y * b.y + (1 - b.x) * (1 - b.x);
                var aGood = aCatDist < aNotCatDist;
                var bGood = bCatDist < bNotCatDist;
                return {aGood: aGood, bGood: bGood};
            }

            function scoreSortForCategory(a, b) {
                var __ret = arePointsPredictiveOfDifferentCategories(a, b);
                if (sortByDist) {
                    var aGood = __ret.aGood;
                    var bGood = __ret.bGood;
                    if (aGood && !bGood) return -1;
                    if (!aGood && bGood) return 1;
                }
                return b.s - a.s;
            }

            function scoreSortForNotCategory(a, b) {
                var __ret = arePointsPredictiveOfDifferentCategories(a, b);
                if (sortByDist) {
                    var aGood = __ret.aGood;
                    var bGood = __ret.bGood;
                    if (aGood && !bGood) return 1;
                    if (!aGood && bGood) return -1;
                }
                if (reverseSortScoresForNotCategory)
                    return a.s - b.s;
                else
                    return b.s - a.s;
            }

            var sortedData = data.map(x => x).sort(sortByDist ? euclideanDistanceSort : scoreSort);
            if (doCensorPoints) {
                for (var i in data) {
                    var d = sortedData[i];
                    censorPoints(
                        d,
                        function (d) {
                            return d.x
                        },
                        function (d) {
                            return d.y
                        }
                    );
                }
            }


            function registerFigureBBox(curLabel) {
                var bbox = curLabel.node().getBBox();
                var borderToRemove = 1.5;
                var x1 = bbox.x + borderToRemove,
                    y1 = bbox.y + borderToRemove,
                    x2 = bbox.x + bbox.width - borderToRemove,
                    y2 = bbox.y + bbox.height - borderToRemove;
                rectHolder.add(new Rectangle(x1, y1, x2, y2));
                //return insertRangeTree(rangeTree, x1, y1, x2, y2, '~~_other_');
            }

            function drawXLabel(svg, labelText) {
                return svg.append("text")
                    .attr("class", "x label")
                    .attr("text-anchor", "end")
                    .attr("x", width)
                    .attr("y", height - 6)
                    .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                    .attr('font-size', '10px')
                    .text(labelText);
            }

            function drawYLabel(svg, labelText) {
                return svg.append("text")
                    .attr("class", "y label")
                    .attr("text-anchor", "end")
                    .attr("y", 6)
                    .attr("dy", ".75em")
                    .attr("transform", "rotate(-90)")
                    .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                    .attr('font-size', '10px')
                    .text(labelText);
                registerFigureBBox(yLabel);
            }

            d3.selection.prototype.moveToBack = function () {
                return this.each(function () {
                    var firstChild = this.parentNode.firstChild;
                    if (firstChild) {
                        this.parentNode.insertBefore(this, firstChild);
                    }
                });
            };

            if (verticalLines) {
                for (i in verticalLines) {
                    svg.append("g")
                        .attr("transform", "translate(" + x(verticalLines) + ", 1)")
                        .append("line")
                        .attr("y2", height)
                        .style("stroke", "#dddddd")
                        .style("stroke-width", "1px")
                        .moveToBack();
                }
            }

            if (showAxes || showAxesAndCrossHairs) {

                var myXAxis = svg.append("g")
                    .attr("class", "x axis")
                    .attr("transform", "translate(0," + height + ")")
                    .call(xAxis);

                //rangeTree = registerFigureBBox(myXAxis);


                var xLabel = drawXLabel(svg, getLabelText('x'));

                //console.log('xLabel');
                //console.log(xLabel);

                //rangeTree = registerFigureBBox(xLabel);
                // Add the Y Axis

                if (!yAxisValues) {
                    var myYAxis = svg.append("g")
                        .attr("class", "y axis")
                        .call(yAxis)
                        .selectAll("text")
                        .style("text-anchor", "end")
                        .attr("dx", "30px")
                        .attr("dy", "-13px")
                        .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                        .attr('font-size', '10px')
                        .attr("transform", "rotate(-90)");
                } else {
                    var myYAxis = svg.append("g")
                        .attr("class", "y axis")
                        .call(yAxis)
                        .selectAll("text")
                        .style("text-anchor", "end")
                        .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                        .attr('font-size', '10px');
                }
                registerFigureBBox(myYAxis);

                function getLabelText(axis) {
                    if (axis == 'y') {
                        if (yLabelText == null)
                            return modelInfo['category_name'] + " Frequency";
                        else
                            return yLabelText;
                    } else {
                        if (xLabelText == null)
                            return modelInfo['not_category_name'] + " Frequency";
                        else
                            return xLabelText;
                    }
                }

                var yLabel = drawYLabel(svg, getLabelText('y'))

            }
            if (!showAxes || showAxesAndCrossHairs) {
                horizontal_line_y_position_translated = 0.5;
                if (horizontal_line_y_position !== null) {
                    var loOy = null, hiOy = null, loY = null, hiY = null;
                    for (i in fullData.data) {
                        var curOy = fullData.data[i].oy;
                        if (curOy < horizontal_line_y_position && (curOy > loOy || loOy === null)) {
                            loOy = curOy;
                            loY = fullData.data[i].y
                        }
                        if (curOy > horizontal_line_y_position && (curOy < hiOy || hiOy === null)) {
                            hiOy = curOy;
                            hiY = fullData.data[i].y
                        }
                    }
                    horizontal_line_y_position_translated = loY + (hiY - loY) / 2.
                    if (loY === null) {
                        horizontal_line_y_position_translated = 0;
                    }
                }
                if (vertical_line_x_position === null) {
                    vertical_line_x_position_translated = 0.5;
                } else {
                    if (vertical_line_x_position !== null) {
                        var loOx = null, hiOx = null, loX = null, hiX = null;
                        for (i in fullData.data) {
                            var curOx = fullData.data[i].ox;
                            if (curOx < vertical_line_x_position && (curOx > loOx || loOx === null)) {
                                loOx = curOx;
                                loX = fullData.data[i].x;
                            }
                            if (curOx > vertical_line_x_position && (curOx < hiOx || hiOx === null)) {
                                hiOx = curOx;
                                hiX = fullData.data[i].x
                            }
                        }
                        vertical_line_x_position_translated = loX + (hiX - loX) / 2.
                        if (loX === null) {
                            vertical_line_x_position_translated = 0;
                        }
                    }
                }
                if (showCrossAxes) {
                    var x_line = svg.append("g")
                        .attr("transform", "translate(0, " + y(horizontal_line_y_position_translated) + ")")
                        .append("line")
                        .attr("x2", width)
                        .style("stroke", "#cccccc")
                        .style("stroke-width", "1px")
                        .moveToBack();
                    var y_line = svg.append("g")
                        .attr("transform", "translate(" + x(vertical_line_x_position_translated) + ", 0)")
                        .append("line")
                        .attr("y2", height)
                        .style("stroke", "#cccccc")
                        .style("stroke-width", "1px")
                        .moveToBack();
                }
            }

            function showWordList(word, termDataList) {
                var maxWidth = word.node().getBBox().width;
                var wordObjList = [];
                for (var i in termDataList) {
                    var curTerm = termDataList[i].term;
                    word = (function (word, curTerm) {
                        var curWordPrinted = svg.append("text")
                            .attr("text-anchor", "start")
                            .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                            .attr('font-size', '12px')
                            .attr("x", word.node().getBBox().x)
                            .attr("y", word.node().getBBox().y
                                + 2 * word.node().getBBox().height)
                            .text(curTerm);
                        wordObjList.push(curWordPrinted)
                        return makeWordInteractive(
                            termDataList, //data,
                            svg,
                            curWordPrinted,
                            curTerm,
                            termDataList[i]);
                    })(word, curTerm);
                    if (word.node().getBBox().width > maxWidth)
                        maxWidth = word.node().getBBox().width;
                    registerFigureBBox(word);
                }
                return {
                    'word': word,
                    'maxWidth': maxWidth,
                    'wordObjList': wordObjList
                };
            }

            function pickEuclideanDistanceSortAlgo(category) {
                if (category == true) return euclideanDistanceSortForCategory;
                return euclideanDistanceSortForNotCategory;
            }

            function pickScoreSortAlgo(category) {
                console.log("PICK SCORE ALGO")
                console.log(category)
                if (category == true) {
                    return scoreSortForCategory;
                } else {
                    return scoreSortForNotCategory;
                }
            }

            function pickTermSortingAlgorithm(category) {
                if (sortByDist) return pickEuclideanDistanceSortAlgo(category);
                return pickScoreSortAlgo(category);
            }

            function showAssociatedWordList(data, word, header, isAssociatedToCategory, length = 14) {
                var sortedData = null;
                var sortingAlgo = pickTermSortingAlgorithm(isAssociatedToCategory);
                sortedData = data.filter(term => (term.display === undefined || term.display === true)).sort(sortingAlgo);
                if (wordVecMaxPValue) {
                    function signifTest(x) {
                        if (isAssociatedToCategory)
                            return x.p >= 1 - minPVal;
                        return x.p <= minPVal;
                    }

                    sortedData = sortedData.filter(signifTest)
                }
                return showWordList(word, sortedData.slice(0, length));

            }

            var characteristicXOffset = width;

            function showCatHeader(startingOffset, catName, registerFigureBBox) {
                var catHeader = svg.append("text")
                    .attr("text-anchor", "start")
                    .attr("x", startingOffset //width
                    )
                    .attr("dy", "6px")
                    .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                    .attr('font-size', '12px')
                    .attr('font-weight', 'bolder')
                    .attr('font-decoration', 'underline')
                    .text(catName
                        //"Top " + fullData['info']['category_name']
                    );
                registerFigureBBox(catHeader);
                return catHeader;
            }

            function showNotCatHeader(startingOffset, word, notCatName) {
                console.log("showNotCatHeader")
                console.log(word)
                console.log(word.node().getBBox().y - word.node().getBBox().height)
                console.log(word.node().getBBox().y + word.node().getBBox().height)
                return svg.append("text")
                    .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                    .attr('font-size', '12px')
                    .attr('font-weight', 'bolder')
                    .attr('font-decoration', 'underline')
                    .attr("text-anchor", "start")
                    .attr("x", startingOffset)
                    .attr("y", word.node().getBBox().y + 3 * word.node().getBBox().height)
                    .text(notCatName);
            }

            function showTopTermsPane(data,
                                      registerFigureBBox,
                                      showAssociatedWordList,
                                      catName,
                                      notCatName,
                                      startingOffset) {
                data = data.filter(term => (term.display === undefined || term.display === true));
                //var catHeader = showCatHeader(startingOffset, catName, registerFigureBBox);
                var catHeader = svg.append("text")
                    .attr("text-anchor", "start")
                    .attr("x", startingOffset)
                    .attr("dy", "6px")
                    .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                    .attr('font-size', '12px')
                    .attr('font-weight', 'bolder')
                    .attr('font-decoration', 'underline')
                    .text(catName
                        //"Top " + fullData['info']['category_name']
                    );
                registerFigureBBox(catHeader);
                var word = catHeader;
                var wordListData = showAssociatedWordList(data, word, catHeader, true);
                word = wordListData.word;
                var maxWidth = wordListData.maxWidth;

                var notCatHeader = showNotCatHeader(startingOffset, word, notCatName);
                word = notCatHeader;
                characteristicXOffset = catHeader.node().getBBox().x + maxWidth + 10;

                var notWordListData = showAssociatedWordList(data, word, notCatHeader, false);
                word = wordListData.word;
                if (wordListData.maxWidth > maxWidth) {
                    maxWidth = wordListData.maxWidth;
                }
                return {
                    wordListData, notWordListData,
                    word, maxWidth, characteristicXOffset, startingOffset,
                    catHeader, notCatHeader, registerFigureBBox
                };
            }

            var payload = Object();
            if (showTopTerms) {
                payload.topTermsPane = showTopTermsPane(
                    data,
                    registerFigureBBox,
                    showAssociatedWordList,
                    "Top " + fullData['info']['category_name'],
                    "Top " + fullData['info']['not_category_name'],
                    width
                );
                payload.showTopTermsPane = showTopTermsPane;
                payload.showAssociatedWordList = showAssociatedWordList;
                payload.showWordList = showWordList;
                /*var wordListData = topTermsPane.wordListData;
                var word = topTermsPane.word;
                var maxWidth = topTermsPane.maxWidth;
                var catHeader = topTermsPane.catHeader;
                var notCatHeader = topTermsPane.notCatHeader;
                var startingOffset = topTermsPane.startingOffset;*/
                characteristicXOffset = payload.topTermsPane.characteristicXOffset;
            }


            if (!nonTextFeaturesMode && !asianMode && showCharacteristic) {
                var sortMethod = backgroundScoreSort;
                var title = 'Characteristic';
                if (wordVecMaxPValue) {
                    title = 'Most similar';
                    sortMethod = scoreSortReverse;
                } else if (data.reduce(function (a, b) {
                    return a + b.bg
                }, 0) === 0) {
                    title = 'Most frequent';
                }
                word = svg.append("text")
                    .attr('font-family', 'Helvetica, Arial, Sans-Serif')
                    .attr("text-anchor", "start")
                    .attr('font-size', '12px')
                    .attr('font-weight', 'bolder')
                    .attr('font-decoration', 'underline')
                    .attr("x", characteristicXOffset)
                    .attr("dy", "6px")
                    .text(title);

                var wordListData = showWordList(word, data.filter(term => (term.display === undefined || term.display === true)).sort(sortMethod).slice(0, 30));

                word = wordListData.word;
                maxWidth = wordListData.maxWidth;
                console.log(maxWidth);
                console.log(word.node().getBBox().x + maxWidth);

                svg.attr('width', word.node().getBBox().x + 3 * maxWidth + 10);
            }

            function performPartialLabeling(data, existingLabels, getX, getY) {
                for (i in existingLabels) {
                    rectHolder.remove(existingLabels[i].rect);
                    existingLabels[i].label.remove();
                }
                console.log('labeling 1')


                var labeledPoints = [];
                //var filteredData = data.filter(d=>d.display === undefined || d.display === true);
                //for (var i = 0; i < filteredData.length; i++) {
                data.forEach(function (datum, i) {
                    //console.log(datum.i, datum.ci, i)
                    //var label = labelPointsIfPossible(i, getX(filteredData[i]), getY(filteredData[i]));
                    if (datum.display === undefined || datum.display === true) {
                        if (datum.term == "the" || i == 1) {
                            console.log("trying to label datum # " + i + ": " + datum.term)
                            console.log(datum)
                            console.log([getX(datum), getY(datum)])
                        }
                        var label = labelPointsIfPossible(datum, getX(datum), getY(datum));
                        if (label !== false) {
                            //console.log("labeled")
                            labeledPoints.push(label)
                        }
                    }
                    //if (labelPointsIfPossible(i), true) numPointsLabeled++;
                })
                return labeledPoints;
            }

            //var labeledPoints = performPartialLabeling();
            var labeledPoints = [];
            labeledPoints = performPartialLabeling(data,
                labeledPoints,
                function (d) {
                    return d.x
                },
                function (d) {
                    return d.y
                });


            /*
            // pointset has to be sorted by X
            function convex(pointset) {
                function _cross(o, a, b) {
                    return (a[0] - o[0]) * (b[1] - o[1]) - (a[1] - o[1]) * (b[0] - o[0]);
                }

                function _upperTangent(pointset) {
                    var lower = [];
                    for (var l = 0; l < pointset.length; l++) {
                        while (lower.length >= 2 && (_cross(lower[lower.length - 2], lower[lower.length - 1], pointset[l]) <= 0)) {
                            lower.pop();
                        }
                        lower.push(pointset[l]);
                    }
                    lower.pop();
                    return lower;
                }

                function _lowerTangent(pointset) {
                    var reversed = pointset.reverse(),
                        upper = [];
                    for (var u = 0; u < reversed.length; u++) {
                        while (upper.length >= 2 && (_cross(upper[upper.length - 2], upper[upper.length - 1], reversed[u]) <= 0)) {
                            upper.pop();
                        }
                        upper.push(reversed[u]);
                    }
                    upper.pop();
                    return upper;
                }

                var convex,
                    upper = _upperTangent(pointset),
                    lower = _lowerTangent(pointset);
                convex = lower.concat(upper);
                convex.push(pointset[0]);
                return convex;
            }

            console.log("POINTSTORE")
            console.log(pointStore);
            pointStore.sort();
            var convexHull = convex(pointStore);
            var minX = convexHull.sort(function (a,b) {
                return a[0] < b[0] ? -1 : 1;
            })[0][0];
            var minY = convexHull.sort(function (a,b) {
                return a[1] < b[1] ? -1 : 1;
            })[0][0];
            //svg.append("text").text("BLAH BLAH").attr("text-anchor", "middle").attr("cx", x(0)).attr("y", minY);
            console.log("POINTSTORE")
            console.log(pointStore);
            console.log(convexHull);
            for (i in convexHull) {
                var i = parseInt(i);
                if (i + 1 == convexHull.length) {
                    var nextI = 0;
                } else {
                    var nextI = i + 1;
                }
                console.log(i, ',', nextI);
                svg.append("line")
                    .attr("x2", width)
                    .style("stroke", "#cc0000")
                    .style("stroke-width", "1px")
                    .attr("x1", convexHull[i][0])     // x position of the first end of the line
                    .attr("y1", convexHull[i][1])      // y position of the first end of the line
                    .attr("x2", convexHull[nextI][0])     // x position of the second end of the line
                    .attr("y2", convexHull[nextI][1]);    // y position of the second end of the line
            }*/

            function populateCorpusStats() {
                var wordCounts = {};
                var docCounts = {}
                fullData.docs.labels.forEach(function (x, i) {
                    var cnt = (
                        fullData.docs.texts[i]
                            .trim()
                            .replace(/['";:,.?¿\-!¡]+/g, '')
                            .match(/\S+/g) || []
                    ).length;
                    var name = null;
                    if (unifiedContexts) {
                        var name = fullData.docs.categories[x];
                        wordCounts[name] = wordCounts[name] ? wordCounts[name] + cnt : cnt;
                    } else {
                        if (fullData.docs.categories[x] == fullData.info.category_internal_name) {
                            name = fullData.info.category_name;
                        } else if (fullData.info.not_category_internal_names.indexOf(fullData.docs.categories[x]) > -1) {
                            name = fullData.info.not_category_name;
                        } else if (fullData.info.neutral_category_internal_names.indexOf(fullData.docs.categories[x]) > -1) {
                            name = fullData.info.neutral_category_name;
                        } else if (fullData.info.extra_category_internal_names.indexOf(fullData.docs.categories[x]) > -1) {
                            name = fullData.info.extra_category_name;
                        }
                        if (name) {
                            wordCounts[name] = wordCounts[name] ? wordCounts[name] + cnt : cnt
                        }
                    }
                    //!!!

                });
                fullData.docs.labels.forEach(function (x) {

                    if (unifiedContexts) {
                        var name = fullData.docs.categories[x];
                        docCounts[name] = docCounts[name] ? docCounts[name] + 1 : 1
                    } else {
                        var name = null;
                        if (fullData.docs.categories[x] == fullData.info.category_internal_name) {
                            name = fullData.info.category_name;
                        } else if (fullData.info.not_category_internal_names.indexOf(fullData.docs.categories[x]) > -1) {
                            name = fullData.info.not_category_name;
                        } else if (fullData.info.neutral_category_internal_names.indexOf(fullData.docs.categories[x]) > -1) {
                            name = fullData.info.neutral_category_name;
                        } else if (fullData.info.extra_category_internal_names.indexOf(fullData.docs.categories[x]) > -1) {
                            name = fullData.info.extra_category_name;
                        }
                        if (name) {
                            docCounts[name] = docCounts[name] ? docCounts[name] + 1 : 1
                        }
                    }
                });
                console.log("docCounts");
                console.log(docCounts)
                var messages = [];
                if (unifiedContexts) {
                    fullData.docs.categories.forEach(function (x, i) {
                        if (docCounts[x] > 0) {
                            messages.push('<b>' + x + '</b> document count: '
                                + Number(docCounts[x]).toLocaleString('en')
                                + '; word count: '
                                + Number(wordCounts[x]).toLocaleString('en'));
                        }
                    });
                } else {
                    [fullData.info.category_name,
                        fullData.info.not_category_name,
                        fullData.info.neutral_category_name,
                        fullData.info.extra_category_name].forEach(function (x, i) {
                        if (docCounts[x] > 0) {
                            messages.push('<b>' + x + '</b> document count: '
                                + Number(docCounts[x]).toLocaleString('en')
                                + '; word count: '
                                + Number(wordCounts[x]).toLocaleString('en'));
                        }
                    });
                }

                if (showCorpusStats) {
                    d3.select('#' + divName + '-' + 'corpus-stats')
                        .style('width', width + margin.left + margin.right + 200)
                        .append('div')
                        .html(messages.join('<br />'));
                }
            }


            if (fullData.docs) {
                populateCorpusStats();
            }

            if (saveSvgButton) {
                // from https://stackoverflow.com/questions/23218174/how-do-i-save-export-an-svg-file-after-creating-an-svg-with-d3-js-ie-safari-an
                var svgElement = document.getElementById(divName);

                var serializer = new XMLSerializer();
                var source = serializer.serializeToString(svgElement);

                if (!source.match(/^<svg[^>]+xmlns="http\:\/\/www\.w3\.org\/2000\/svg"/)) {
                    source = source.replace(/^<svg/, '<svg xmlns="https://www.w3.org/2000/svg"');
                }
                if (!source.match(/^<svg[^>]+"http\:\/\/www\.w3\.org\/1999\/xlink"/)) {
                    source = source.replace(/^<svg/, '<svg xmlns:xlink="https://www.w3.org/1999/xlink"');
                }

                source = '<?xml version="1.0" standalone="no"?>\r\n' + source;

                var url = "data:image/svg+xml;charset=utf-8," + encodeURIComponent(source);

                var downloadLink = document.createElement("a");
                downloadLink.href = url;
                downloadLink.download = fullData['info']['category_name'] + ".svg";
                downloadLink.innerText = 'Download SVG';
                document.body.appendChild(downloadLink);

            }

            function rerender(xCoords, yCoords, color) {
                labeledPoints.forEach(function (p) {
                    p.label.remove();
                    rectHolder.remove(p.rect);
                });
                pointRects.forEach(function (rect) {
                    rectHolder.remove(rect);
                });
                pointRects = []
                /*
                var circles = d3.select('#' + divName).selectAll('circle')
                    .attr("cy", function (d) {return y(yCoords[d.i])})
                    .transition(0)
                    .attr("cx", function (d) {return x(xCoords[d.i])})
                    .transition(0);
                */
                d3.select('#' + divName).selectAll("dot").remove();
                d3.select('#' + divName).selectAll("circle").remove();
                console.log(fullData)
                console.log(this)
                var circles = this.svg//.select('#' + divName)
                    .selectAll("dot")
                    .data(this.fullData.data.filter(d => d.display === undefined || d.display === true))
                    //.filter(function (d) {return d.display === undefined || d.display === true})
                    .enter()
                    .append("circle")
                    .attr("cy", d => d.y)
                    .attr("cx", d => d.x)
                    .attr("r", d => 2)
                    .on("mouseover", function (d) {
                        /*var mySVGMatrix = circle.getScreenCTM()n
                            .translate(circle.cx.baseVal.value, circle.cy.baseVal.value);
                        var pageX = mySVGMatrix.e;
                        var pageY = mySVGMatrix.f;*/

                        /*showTooltip(
                            d,
                            d3.event.pageX,
                            d3.event.pageY
                        );*/
                        console.log("point MOUSOEVER")
                        console.log(d)
                        showToolTipForTerm(data, this, d.term, d, true);
                        d3.select(this).style("stroke", "black");
                    })
                    .on("click", function (d) {
                        var runDisplayTermContexts = true;
                        if (alternativeTermFunc != null) {
                            runDisplayTermContexts = alternativeTermFunc(d);
                        }
                        if (runDisplayTermContexts) {
                            displayTermContexts(data, gatherTermContexts(d), true, includeAllContexts);
                        }
                    })
                    .on("mouseout", function (d) {
                        tooltip.transition()
                            .duration(0)
                            .style("opacity", 0);
                        d3.select(this).style("stroke", null);
                        d3.select('#' + divName + '-' + 'overlapped-terms')
                            .selectAll('div')
                            .remove();
                    });

                if (color !== null) {
                    circles.style("fill", d => color(d));
                }
                xCoords.forEach((xCoord, i) => censorCircle(xCoord, yCoords[i]))
                labeledPoints = [];
                labeledPoints = performPartialLabeling(
                    this.fullData.data,
                    labeledPoints,
                    (d => d.ox), //function (d) {return xCoords[d.ci]},
                    (d => d.oy) //function (d) {return yCoords[d.ci]}
                );
            }

            //return [performPartialLabeling, labeledPoints];
            return {
                ...payload,
                ...{
                    'rerender': rerender,
                    'performPartialLabeling': performPartialLabeling,
                    'showToolTipForTerm': showToolTipForTerm,
                    'svg': svg,
                    'data': data,
                    'xLabel': xLabel,
                    'yLabel': yLabel,
                    'drawXLabel': drawXLabel,
                    'drawYLabel': drawYLabel,
                    'populateCorpusStats': populateCorpusStats
                }
            };
        }


        //fullData = getDataAndInfo();
        if (fullData.docs) {
            var corpusWordCounts = getCorpusWordCounts();
        }
        var payload = processData(fullData);

        // The tool tip is down here in order to make sure it has the highest z-index
        var tooltip = d3.select('#' + divName)
            .append("div")
            //.attr("class", getTooltipContent == null && sortByDist ? "tooltip" : "tooltipscore")
            .attr("class", "tooltipscore")
            .style("opacity", 0);

        plotInterface = {}
        if (payload.topTermsPane) {
            plotInterface.topTermsPane = payload.topTermsPane;
            plotInterface.showTopTermsPane = payload.showTopTermsPane;
            plotInterface.showAssociatedWordList = payload.showAssociatedWordList;
        }
        plotInterface.includeAllContexts = includeAllContexts;
        plotInterface.divName = divName;
        plotInterface.displayTermContexts = displayTermContexts;
        plotInterface.gatherTermContexts = gatherTermContexts;
        plotInterface.xLabel = payload.xLabel;
        plotInterface.yLabel = payload.yLabel;
        plotInterface.drawXLabel = payload.drawXLabel;
        plotInterface.drawYLabel = payload.drawYLabel;
        plotInterface.svg = payload.svg;
        plotInterface.termDict = termDict;
        plotInterface.showToolTipForTerm = payload.showToolTipForTerm;
        plotInterface.fullData = fullData;
        plotInterface.data = payload.data;
        plotInterface.rerender = payload.rerender;
        plotInterface.populateCorpusStats = payload.populateCorpusStats;
        plotInterface.handleSearch = handleSearch;
        plotInterface.handleSearchTerm = handleSearchTerm;
        plotInterface.highlightTerm = highlightTerm;
        plotInterface.y = y;
        plotInterface.x = x;
        plotInterface.tooltip = tooltip;
        plotInterface.alternativeTermFunc = alternativeTermFunc;

        plotInterface.showTooltipSimple = function (term) {
            plotInterface.showToolTipForTerm(
                plotInterface.data,
                plotInterface.svg,
                term.replace("'", "\\'"),
                plotInterface.termDict[term.replace("'", "\\'")]
            )
        };

        plotInterface.drawCategoryAssociation = function (categoryNum, otherCategoryNum = null) {
            var rawLogTermCounts = getTermCounts(this.fullData).map(Math.log);
            var maxRawLogTermCounts = Math.max(...rawLogTermCounts);
            var minRawLogTermCounts = Math.min(...rawLogTermCounts);
            var logTermCounts = rawLogTermCounts.map(
                x => (x - minRawLogTermCounts) / maxRawLogTermCounts
            )

            //var rawScores = getCategoryDenseRankScores(this.fullData, categoryNum);
            //console.log("RAW SCORES")
            //console.log(rawScores);
            /*
            function logOddsRatioUninformativeDirichletPrior(fgFreqs, bgFreqs, alpha) {
                var fgVocabSize = fgFreqs.reduce((x,y) => x+y);
                var fgL = fgFreqs.map(x => (x + alpha)/((1+alpha)*fgVocabSize - x - alpha))
                var bgVocabSize = bgFreqs.reduce((x,y) => x+y);
                var bgL = bgFreqs.map(x => (x + alpha)/((1+alpha)*bgVocabSize - x - alpha))
                var pooledVar = fgFreqs.map(function(x, i) {
                    return (
                        1/(x + alpha)
                        + 1/((1+alpha)*fgVocabSize - x - alpha)
                        + 1/(bgFreqs[i] + alpha)
                        + 1/((1+alpha)*bgVocabSize - bgFreqs[i] - alpha))
                })
                return pooledVar.map(function(x, i) {
                    return (Math.log(fgL[i]) - Math.log(bgL[i]))/x;
                })
            }
            var rawScores = logOddsRatioUninformativeDirichletPrior(
                denseRanks.fgFreqs, denseRanks.bgFreqs, 0.01);
            */


            var denseRanks = getDenseRanks(this.fullData, categoryNum)
            console.log("denseRanks")
            console.log(denseRanks);
            if (otherCategoryNum !== null) {
                var otherDenseRanks = getDenseRanks(this.fullData, otherCategoryNum);
                console.log("otherDenseRanks");
                console.log(otherDenseRanks);
                denseRanks.bg = otherDenseRanks.fg;
                denseRanks.bgFreqs = otherDenseRanks.fgFreqs;

            }

            var rawScores = denseRanks.fg.map((x, i) => x - denseRanks.bg[i]);
            var minRawScores = Math.min(...rawScores);
            var maxRawScores = Math.max(...rawScores);

            var scores = rawScores.map(
                function (rawScore) {
                    if (rawScore == 0) {
                        return 0.5;
                    } else if (rawScore > 0) {
                        return rawScore / (2. * maxRawScores) + 0.5;
                    } else if (rawScore < 0) {
                        return 0.5 - rawScore / (2. * minRawScores);
                    }
                }
            )
            var fgFreqSum = denseRanks.fgFreqs.reduce((a, b) => a + b, 0)
            var bgFreqSum = denseRanks.bgFreqs.reduce((a, b) => a + b, 0)

            //!!! OLD and good
            var ox = denseRanks.bg;
            var oy = denseRanks.fg;

            //!!! NEW
            /*
            var oy = denseRanks.fg.map((x,i)=> x - denseRanks.bg[i]);
            var ox = denseRanks.fgFreqs.map((x,i)=> x/fgFreqSum - denseRanks.bgFreqs[i]/bgFreqSum);
            */
            /*

            var ox = denseRanks.fg;
            */

            /*
            ox = ox.map(function(x) {
                if (x > 0)
                    return 0.5 * x/Math.max(...ox) + 0.5;
                else
                    return 0.5 * (1 + x/Math.min(...ox));

            })
            oy = oy.map(function(x) {
                if (x > 0)
                    return 0.5 * x/Math.max(...oy) + 0.5;
                else
                    return 0.5 * (1 + x/Math.min(...oy));

            })*/


            var oxmax = Math.max(...ox)
            var oxmin = Math.min(...ox)
            var ox = ox.map(x => (x - oxmin) / (oxmax - oxmin))
            var oymax = Math.max(...oy)
            var oymin = Math.min(...oy)
            var oy = oy.map(x => (x - oymin) / (oymax - oymin))
            //var ox = logTermCounts
            //var oy = scores;
            var xf = this.x;
            var yf = this.y;

            this.fullData.data = this.fullData.data.map(function (term, i) {
                //term.ci = i;
                term.s = scores[i];
                term.os = rawScores[i];
                term.cat = denseRanks.fgFreqs[i];
                term.ncat = denseRanks.bgFreqs[i];
                term.cat25k = parseInt(denseRanks.fgFreqs[i] * 25000 / fgFreqSum);
                term.ncat25k = parseInt(denseRanks.bgFreqs[i] * 25000 / bgFreqSum);
                term.x = xf(ox[i]) // logTermCounts[term.i];
                term.y = yf(oy[i]) // scores[term.i];
                term.ox = ox[i];
                term.oy = oy[i];
                term.display = false;
                return term;
            })

            // Feature selection
            var targetTermsToShow = 1500;

            var sortedBg = denseRanks.bg.map((x, i) => [x, i]).sort((a, b) => b[0] - a[0]).map(x => x[1]).slice(0, parseInt(targetTermsToShow / 2));
            var sortedFg = denseRanks.fg.map((x, i) => [x, i]).sort((a, b) => b[0] - a[0]).map(x => x[1]).slice(0, parseInt(targetTermsToShow / 2));
            var sortedScores = denseRanks.fg.map((x, i) => [x, i]).sort((a, b) => b[0] - a[0]).map(x => x[1]);
            var myFullData = this.fullData

            sortedBg.concat(sortedFg)//.concat(sortedScores.slice(0, parseInt(targetTermsToShow/2))).concat(sortedScores.slice(-parseInt(targetTermsToShow/4)))
                .forEach(function (i) {
                    myFullData.data[i].display = true;
                })

            console.log('newly filtered')
            console.log(myFullData)

            // begin rescaling to ignore hidden terms
            /*
            function scaleDenseRanks(ranks) {
                var max = Math.max(...ranks);
                return ranks.map(x=>x/max)
            }
            var filteredData = myFullData.data.filter(d=>d.display);
            var catRanks = scaleDenseRanks(denseRank(filteredData.map(d=>d.cat)))
            var ncatRanks = scaleDenseRanks(denseRank(filteredData.map(d=>d.ncat)))
            var rawScores = catRanks.map((x,i) => x - ncatRanks[i]);
            function stretch_0_1(scores) {
                var max = 1.*Math.max(...rawScores);
                var min = -1.*Math.min(...rawScores);
                return scores.map(function(x, i) {
                    if(x == 0) return 0.5;
                    if(x > 0) return (x/max + 1)/2;
                    return (x/min + 1)/2;
                })
            }
            var scores = stretch_0_1(rawScores);
            console.log(scores)
            filteredData.forEach(function(d, i) {
                d.x = xf(catRanks[i]);
                d.y = yf(ncatRanks[i]);
                d.ox = catRanks[i];
                d.oy = ncatRanks[i];
                d.s = scores[i];
                d.os = rawScores[i];
            });
            console.log("rescaled");
            */
            // end rescaling


            this.rerender(//denseRanks.bg,
                fullData.data.map(x => x.ox), //ox
                //denseRanks.fg,
                fullData.data.map(x => x.oy), //oy,
                d => d3.interpolateRdYlBu(d.s));
            this.yLabel.remove()
            this.xLabel.remove()

            var leftName = this.fullData.info.categories[categoryNum];
            var bottomName = "Not " + this.fullData.info.categories[categoryNum];
            if (otherCategoryNum !== null) {
                bottomName = this.fullData.info.categories[otherCategoryNum];
            }


            this.yLabel = this.drawYLabel(this.svg, leftName + ' Frequncy Rank')
            this.xLabel = this.drawXLabel(this.svg, bottomName + ' Frequency Rank')
            console.log(this.topTermsPane)
            this.topTermsPane.catHeader.remove()
            this.topTermsPane.notCatHeader.remove()
            this.topTermsPane.wordListData.wordObjList.map(x => x.remove())
            this.topTermsPane.notWordListData.wordObjList.map(x => x.remove())
            this.showWordList = payload.showWordList;


            this.showAssociatedWordList = function (data, word, header, isAssociatedToCategory, length = 14) {
                var sortedData = null;
                if (!isAssociatedToCategory) {
                    sortedData = data.map(x => x).sort((a, b) => scores[a.i] - scores[b.i])
                } else {
                    sortedData = data.map(x => x).sort((a, b) => scores[b.i] - scores[a.i])
                }
                console.log('sortedData');
                console.log(isAssociatedToCategory);
                console.log(sortedData.slice(0, length))
                console.log(payload)
                console.log(word)
                return payload.showWordList(word, sortedData.slice(0, length));
            }
            this.topTermsPane = payload.showTopTermsPane(
                this.data,
                this.topTermsPane.registerFigureBBox,
                this.showAssociatedWordList,
                "Top " + leftName,
                "Top " + bottomName,
                this.topTermsPane.startingOffset
            )

            fullData.info.category_name = leftName;
            fullData.info.not_category_name = bottomName;
            fullData.info.category_internal_name = this.fullData.info.categories[categoryNum];
            if (otherCategoryNum === null) {
                fullData.info.not_category_internal_names = this.fullData.info.categories
                    .filter(x => x !== this.fullData.info.categories[categoryNum]);
            } else {
                fullData.info.not_category_internal_names = this.fullData.info.categories
                    .filter(x => x === this.fullData.info.categories[otherCategoryNum]);

                fullData.info.neutral_category_internal_names = this.fullData.info.categories
                    .filter(x => (x !== this.fullData.info.categories[categoryNum]
                        && x !== this.fullData.info.categories[otherCategoryNum]));
                fullData.info.neutral_category_name = "All Others";

            }
            console.log("fullData.info.not_category_internal_names");
            console.log(fullData.info.not_category_internal_names);
            ['snippets', 'snippetsalt', 'termstats',
                'overlapped-terms-clicked', 'categoryinfo',
                'cathead', 'cat', 'corpus-stats', 'notcathead',
                'notcat', 'neuthead', 'neut'
            ].forEach(function (divSubName) {
                var mydiv = '#' + divName + '-' + divSubName;
                console.log("Clearing");
                console.log(mydiv);
                d3.select(mydiv).selectAll("*").remove();
                d3.select(mydiv).html("");

            });
            this.populateCorpusStats();
            console.log(fullData)
        };

        return plotInterface
    };
}(d3);

; 
 
 // Adapted from https://www.w3schools.com/howto/howto_js_autocomplete.asp
function autocomplete(inputField, autocompleteValues, myPlotInterface) {
    var currentFocus; // current position in autocomplete list.

    inputField.addEventListener("input", function (e) {
        var matchedCandidateListDiv, matchedCandidateDiv, i, userInput = this.value;

        closeAllLists();
        if (!userInput) {
            return false;
        }
        currentFocus = -1;

        matchedCandidateListDiv = document.createElement("div");
        matchedCandidateListDiv.setAttribute("id", this.id + "autocomplete-list");
        matchedCandidateListDiv.setAttribute("class", "autocomplete-items");

        this.parentNode.appendChild(matchedCandidateListDiv);
        autocompleteValues.map(function (candidate) {
            var candidatePrefix = candidate.substr(0, userInput.length);
            if (candidatePrefix.toLowerCase() === userInput.toLowerCase()) {
                matchedCandidateDiv = document.createElement("div");
                matchedCandidateDiv.innerHTML = "<strong>" + candidatePrefix + "</strong>";
                matchedCandidateDiv.innerHTML += candidate.substr(userInput.length);
                matchedCandidateDiv.innerHTML += "<input type='hidden' value='" + candidate + "'>";
                matchedCandidateDiv.addEventListener("click", function (e) {
                    inputField.value = this.getElementsByTagName("input")[0].value;
                    closeAllLists();
                    myPlotInterface.handleSearchTerm(inputField.value);
                });
                matchedCandidateListDiv.appendChild(matchedCandidateDiv);
            }
        });
    });

    inputField.addEventListener("keydown", function (keyboardEvent) {

        var candidateDivList = document.getElementById(this.id + "autocomplete-list");

        if (!candidateDivList)
            return true;

        var selectedCandidate = Array.prototype.find.call(
            candidateDivList.children,
            x => x.className !== ""
        );

        if (keyboardEvent.keyCode === 40 || keyboardEvent.keyCode === 9) { // down or tab
            keyboardEvent.preventDefault();
            currentFocus++;
            addActive(candidateDivList.getElementsByTagName("div"));
        } else if (keyboardEvent.keyCode === 38) { //up
            currentFocus--;
            addActive(candidateDivList.getElementsByTagName("div"));
        } else if (keyboardEvent.keyCode === 13) { // enter
            keyboardEvent.preventDefault();
            var selectedTerm = inputField.value;
            console.log("selected term");console.log(selectedTerm);
            console.log(myPlotInterface);
            //if (selectedCandidate)
            //    selectedTerm = selectedCandidate.children[1].value;
            myPlotInterface.handleSearchTerm(selectedTerm);
            closeAllLists(null);
        } else if (keyboardEvent.keyCode === 27) { // esc
            closeAllLists(null);
        }
    });

    function addActive(candidateDivList) {
        if (!candidateDivList) return false;

        removeActive(candidateDivList);

        if (currentFocus >= candidateDivList.length)
            currentFocus = 0;
        if (currentFocus < 0)
            currentFocus = (candidateDivList.length - 1);

        candidateDivList[currentFocus].classList.add("autocomplete-active");

        var selectedCandidate = Array.prototype.find.call(
            candidateDivList,
            x => x.className !== ""
        );

        if (selectedCandidate) {
            var candidateValue = selectedCandidate.children[1].value;
            myPlotInterface.highlightTerm(candidateValue);
            inputField.value = candidateValue;
        }

    }

    function removeActive(candidateDivList) {
        Array.prototype.find.call(
            candidateDivList,
            x => x.classList.remove("autocomplete-active")
        );
    }

    function closeAllLists(elmnt) {
        /*close all autocomplete lists in the document,
        except the one passed as an argument:*/
        var x = document.getElementsByClassName("autocomplete-items");
        for (var i = 0; i < x.length; i++) {
            if (elmnt != x[i] && elmnt != inputField) {
                x[i].parentNode.removeChild(x[i]);
            }
        }
    }

    /*execute a function when someone clicks in the document:*/
    document.addEventListener("click", function (e) {
        closeAllLists(e.target);
    });
}

function getDataAndInfo() { return{"info": {"category_name": "Best", "not_category_name": "Worst", "category_terms": ["just", "difficult", "n't", "difficult to", "not", "hard", "without", "do", "none", "do n't"], "not_category_terms": ["just", "difficult", "n't", "difficult to", "not", "hard", "without", "do", "none", "do n't"], "category_internal_name": "best", "not_category_internal_names": ["worst"], "categories": ["best", "worst"], "neutral_category_internal_names": [], "extra_category_internal_names": [], "neutral_category_name": "Neutral", "extra_category_name": "Extra"}, "data": [{"x": 0.6793103448275862, "y": 0.7758620689655172, "ox": 0.6793103448275862, "oy": 0.7758620689655172, "term": "which", "cat25k": 91, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 23, "ncat": 14, "s": 0.8448275862068966, "os": 0.09212652966982221, "bg": 9.129861442866252e-08}, {"x": 0.896551724137931, "y": 0.8103448275862069, "ox": 0.896551724137931, "oy": 0.8103448275862069, "term": "online", "cat25k": 115, "ncat25k": 179, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 29, "ncat": 37, "s": 0.05862068965517241, "os": -0.15123528053567303, "bg": 2.1951337908269317e-07}, {"x": 0.35517241379310344, "y": 0.2655172413793103, "ox": 0.35517241379310344, "oy": 0.2655172413793103, "term": "instructional", "cat25k": 28, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 7, "s": 0.396551724137931, "os": -0.018471484645578393, "bg": 2.8976553311424985e-06}, {"x": 0.6206896551724138, "y": 0.6413793103448275, "ox": 0.6206896551724138, "oy": 0.6413793103448275, "term": "methods", "cat25k": 60, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 15, "ncat": 12, "s": 0.5448275862068965, "os": 0.0122373585776957, "bg": 6.142598373712955e-07}, {"x": 0.9827586206896551, "y": 0.9827586206896551, "ox": 0.9827586206896551, "oy": 0.9827586206896551, "term": "have", "cat25k": 536, "ncat25k": 545, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 135, "ncat": 113, "s": 0.5310344827586206, "os": 0.011544677903486456, "bg": 3.1709176464912474e-07}, {"x": 0.8758620689655172, "y": 0.9172413793103448, "ox": 0.8758620689655172, "oy": 0.9172413793103448, "term": "worked", "cat25k": 226, "ncat25k": 159, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 57, "ncat": 33, "s": 0.9275862068965518, "os": 0.16555068113599625, "bg": 4.719296134809944e-06}, {"x": 0.1, "y": 0.906896551724138, "ox": 0.1, "oy": 0.906896551724138, "term": "best", "cat25k": 206, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 52, "ncat": 4, "s": 1.0, "os": 0.5659201108289079, "bg": 3.011839468343213e-07}, {"x": 0.9551724137931035, "y": 0.9793103448275862, "ox": 0.9551724137931035, "oy": 0.9793103448275862, "term": "for", "cat25k": 500, "ncat25k": 376, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 126, "ncat": 78, "s": 0.8724137931034482, "os": 0.11221426922188871, "bg": 6.876402704199432e-08}, {"x": 0.5793103448275863, "y": 0.15172413793103448, "ox": 0.5793103448275863, "oy": 0.15172413793103448, "term": "you", "cat25k": 20, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 11, "s": 0.08620689655172414, "os": -0.11221426922188871, "bg": 1.0680216279693071e-08}, {"x": 0.2655172413793103, "y": 0.06551724137931035, "ox": 0.2655172413793103, "oy": 0.06551724137931035, "term": "instructional methods", "cat25k": 16, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 6, "s": 0.2724137931034483, "os": -0.04433156314938813, "bg": 0.0}, {"x": 0.3586206896551724, "y": 0.8379310344827586, "ox": 0.3586206896551724, "oy": 0.8379310344827586, "term": "have worked", "cat25k": 131, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 33, "ncat": 7, "s": 0.993103448275862, "os": 0.34772569845301315, "bg": 0.0}, {"x": 0.0, "y": 0.6448275862068965, "ox": 0.0, "oy": 0.6448275862068965, "term": "worked best", "cat25k": 60, "ncat25k": 0, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 15, "ncat": 0, "s": 0.9517241379310344, "os": 0.20895867005310553, "bg": 0.0}, {"x": 0.0034482758620689655, "y": 0.7793103448275862, "ox": 0.0034482758620689655, "oy": 0.7793103448275862, "term": "best for", "cat25k": 91, "ncat25k": 0, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 23, "ncat": 0, "s": 0.9896551724137932, "os": 0.32163472639113366, "bg": 0.0}, {"x": 0.906896551724138, "y": 0.9310344827586207, "ox": 0.906896551724138, "oy": 0.9310344827586207, "term": "with", "cat25k": 234, "ncat25k": 203, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 59, "ncat": 42, "s": 0.8517241379310344, "os": 0.09535903948279845, "bg": 6.345967560046544e-08}, {"x": 0.9379310344827586, "y": 0.9551724137931035, "ox": 0.9379310344827586, "oy": 0.9551724137931035, "term": "my", "cat25k": 329, "ncat25k": 289, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 83, "ncat": 60, "s": 0.8551724137931034, "os": 0.09558993304086816, "bg": 2.6986057056343023e-07}, {"x": 0.803448275862069, "y": 0.6586206896551724, "ox": 0.803448275862069, "oy": 0.6586206896551724, "term": "professors", "cat25k": 64, "ncat25k": 111, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 23, "s": 0.06551724137931035, "os": -0.13761256060955898, "bg": 1.7151282003357697e-05}, {"x": 1.0, "y": 1.0, "ox": 1.0, "oy": 1.0, "term": "the", "cat25k": 1107, "ncat25k": 941, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 279, "ncat": 195, "s": 0.46551724137931033, "os": 0.0, "bg": 4.0975343534774345e-08}, {"x": 0.4482758620689655, "y": 0.7172413793103448, "ox": 0.4482758620689655, "oy": 0.7172413793103448, "term": "since", "cat25k": 75, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 19, "ncat": 8, "s": 0.896551724137931, "os": 0.13414915723851306, "bg": 2.519644854378012e-07}, {"x": 0.9241379310344827, "y": 0.9103448275862069, "ox": 0.9241379310344827, "oy": 0.9103448275862069, "term": "all", "cat25k": 210, "ncat25k": 222, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 53, "ncat": 46, "s": 0.4275862068965517, "os": -0.010159316555068076, "bg": 9.789995150253958e-08}, {"x": 0.9413793103448276, "y": 0.9655172413793104, "ox": 0.9413793103448276, "oy": 0.9655172413793104, "term": "classes", "cat25k": 385, "ncat25k": 294, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 97, "ncat": 61, "s": 0.8758620689655172, "os": 0.12145001154467783, "bg": 6.468769140826885e-06}, {"x": 0.9448275862068966, "y": 0.9379310344827586, "ox": 0.9448275862068966, "oy": 0.9379310344827586, "term": "are", "cat25k": 274, "ncat25k": 323, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 69, "ncat": 67, "s": 0.4310344827586207, "os": -0.0076194874163010295, "bg": 1.1363503572627661e-07}, {"x": 0.8517241379310345, "y": 0.9, "ox": 0.8517241379310345, "oy": 0.9, "term": "discussion", "cat25k": 183, "ncat25k": 140, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 46, "ncat": 29, "s": 0.9172413793103448, "os": 0.16070191641653192, "bg": 1.3394470937418123e-06}, {"x": 0.3620689655172414, "y": 0.2689655172413793, "ox": 0.3620689655172414, "oy": 0.2689655172413793, "term": "based", "cat25k": 28, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 7, "s": 0.396551724137931, "os": -0.018471484645578393, "bg": 1.1092703254265958e-07}, {"x": 0.9896551724137931, "y": 0.9896551724137931, "ox": 0.9896551724137931, "oy": 0.9896551724137931, "term": "and", "cat25k": 802, "ncat25k": 685, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 202, "ncat": 142, "s": 0.5103448275862068, "os": 0.0069268067420918955, "bg": 5.2932640324280435e-08}, {"x": 0.7551724137931034, "y": 0.8448275862068966, "ox": 0.7551724137931034, "oy": 0.8448275862068966, "term": "can", "cat25k": 135, "ncat25k": 82, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 34, "ncat": 17, "s": 0.9448275862068966, "os": 0.1978757792657585, "bg": 8.210335828372558e-08}, {"x": 0.8793103448275862, "y": 0.8275862068965517, "ox": 0.8793103448275862, "oy": 0.8275862068965517, "term": "be", "cat25k": 123, "ncat25k": 159, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 31, "ncat": 33, "s": 0.1793103448275862, "os": -0.07388593858231357, "bg": 5.336141052894527e-08}, {"x": 0.36551724137931035, "y": 0.06896551724137931, "ox": 0.36551724137931035, "oy": 0.06896551724137931, "term": "groups", "cat25k": 16, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 7, "s": 0.19655172413793104, "os": -0.060725005772338955, "bg": 1.7484289948242765e-07}, {"x": 0.1724137931034483, "y": 0.35172413793103446, "ox": 0.1724137931034483, "oy": 0.35172413793103446, "term": "my professors", "cat25k": 32, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 5, "s": 0.6172413793103448, "os": 0.02839990764257677, "bg": 0.0}, {"x": 0.5137931034482759, "y": 0.15517241379310345, "ox": 0.5137931034482759, "oy": 0.15517241379310345, "term": "can be", "cat25k": 20, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 9, "s": 0.1517241379310345, "os": -0.07942738397598706, "bg": 0.0}, {"x": 0.8413793103448276, "y": 0.8, "ox": 0.8413793103448276, "oy": 0.8, "term": "moodle", "cat25k": 107, "ncat25k": 125, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 27, "ncat": 26, "s": 0.3310344827586207, "os": -0.03186331101362272, "bg": 0.00010469342604298356}, {"x": 0.17586206896551723, "y": 0.07241379310344828, "ox": 0.17586206896551723, "oy": 0.07241379310344828, "term": "writing", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 2.163989765242095e-07}, {"x": 0.7793103448275862, "y": 0.8068965517241379, "ox": 0.7793103448275862, "oy": 0.8068965517241379, "term": "discussions", "cat25k": 111, "ncat25k": 101, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 28, "ncat": 21, "s": 0.7620689655172413, "os": 0.06418840914338492, "bg": 3.062623653430007e-06}, {"x": 0.9103448275862069, "y": 0.9241379310344827, "ox": 0.9103448275862069, "oy": 0.9241379310344827, "term": "recorded", "cat25k": 230, "ncat25k": 207, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 58, "ncat": 43, "s": 0.7655172413793103, "os": 0.064881089817594, "bg": 7.759795454864996e-06}, {"x": 0.9586206896551724, "y": 0.9758620689655172, "ox": 0.9586206896551724, "oy": 0.9758620689655172, "term": "lectures", "cat25k": 453, "ncat25k": 396, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 114, "ncat": 82, "s": 0.806896551724138, "os": 0.08173631955668437, "bg": 4.375143559398042e-05}, {"x": 0.8206896551724138, "y": 0.8586206896551725, "ox": 0.8206896551724138, "oy": 0.8586206896551725, "term": "recorded lectures", "cat25k": 143, "ncat25k": 116, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 36, "ncat": 24, "s": 0.8896551724137931, "os": 0.1276841376125606, "bg": 0.0}, {"x": 0.9758620689655172, "y": 0.9620689655172414, "ox": 0.9758620689655172, "oy": 0.9620689655172414, "term": "a", "cat25k": 373, "ncat25k": 453, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 94, "ncat": 94, "s": 0.2862068965517241, "os": -0.040175479104132994, "bg": 4.1404275098063926e-08}, {"x": 0.9862068965517241, "y": 0.9724137931034482, "ox": 0.9862068965517241, "oy": 0.9724137931034482, "term": "of", "cat25k": 437, "ncat25k": 603, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 110, "ncat": 125, "s": 0.2655172413793103, "os": -0.04710228584622489, "bg": 3.573612935274929e-08}, {"x": 0.7379310344827587, "y": 0.7896551724137931, "ox": 0.7379310344827587, "oy": 0.7896551724137931, "term": "them", "cat25k": 99, "ncat25k": 77, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 25, "ncat": 16, "s": 0.8379310344827586, "os": 0.08750865850842765, "bg": 2.0346717141677694e-07}, {"x": 0.04827586206896552, "y": 0.7206896551724138, "ox": 0.04827586206896552, "oy": 0.7206896551724138, "term": "works", "cat25k": 75, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 19, "ncat": 3, "s": 0.9586206896551724, "os": 0.21611637035326714, "bg": 4.46271520620001e-07}, {"x": 0.8655172413793103, "y": 0.8827586206896552, "ox": 0.8655172413793103, "oy": 0.8827586206896552, "term": "because", "cat25k": 167, "ncat25k": 154, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 42, "ncat": 32, "s": 0.7758620689655172, "os": 0.06926806742091896, "bg": 5.454471242912757e-07}, {"x": 0.9724137931034482, "y": 0.9517241379310345, "ox": 0.9724137931034482, "oy": 0.9517241379310345, "term": "it", "cat25k": 310, "ncat25k": 434, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 78, "ncat": 90, "s": 0.1896551724137931, "os": -0.06603555760794266, "bg": 1.1943791633584896e-07}, {"x": 0.9517241379310345, "y": 0.9482758620689655, "ox": 0.9517241379310345, "oy": 0.9482758620689655, "term": "class", "cat25k": 302, "ncat25k": 367, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 76, "ncat": 76, "s": 0.4758620689655172, "os": 0.0018471484645578018, "bg": 1.5907827701983258e-06}, {"x": 0.8310344827586207, "y": 0.8482758620689655, "ox": 0.8310344827586207, "oy": 0.8482758620689655, "term": "more", "cat25k": 135, "ncat25k": 121, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 34, "ncat": 25, "s": 0.8137931034482758, "os": 0.08312168090510275, "bg": 7.638604928515809e-08}, {"x": 0.5827586206896552, "y": 0.6482758620689655, "ox": 0.5827586206896552, "oy": 0.6482758620689655, "term": "of them", "cat25k": 60, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 15, "ncat": 11, "s": 0.6241379310344828, "os": 0.02863080120064651, "bg": 0.0}, {"x": 0.1793103448275862, "y": 0.5793103448275863, "ox": 0.1793103448275862, "oy": 0.5793103448275863, "term": "because it", "cat25k": 48, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 12, "ncat": 5, "s": 0.8206896551724138, "os": 0.08473793581159086, "bg": 0.0}, {"x": 0.993103448275862, "y": 0.996551724137931, "ox": 0.993103448275862, "oy": 0.996551724137931, "term": "i", "cat25k": 977, "ncat25k": 878, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 246, "ncat": 182, "s": 0.5862068965517242, "os": 0.018702378203648173, "bg": 2.773602729823873e-07}, {"x": 0.9275862068965517, "y": 0.8310344827586207, "ox": 0.9275862068965517, "oy": 0.8310344827586207, "term": "do", "cat25k": 127, "ncat25k": 256, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 32, "ncat": 53, "s": 0.024137931034482755, "os": -0.22373585776956822, "bg": 1.7880342752118713e-07}, {"x": 0.7827586206896552, "y": 0.7931034482758621, "ox": 0.7827586206896552, "oy": 0.7931034482758621, "term": "really", "cat25k": 103, "ncat25k": 101, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 26, "ncat": 21, "s": 0.6689655172413793, "os": 0.03601939505887786, "bg": 5.800807598307551e-07}, {"x": 0.8241379310344827, "y": 0.8931034482758621, "ox": 0.8241379310344827, "oy": 0.8931034482758621, "term": "like", "cat25k": 179, "ncat25k": 116, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 45, "ncat": 24, "s": 0.9551724137931034, "os": 0.21219117986608171, "bg": 2.6507961019720616e-07}, {"x": 0.18275862068965518, "y": 0.5137931034482759, "ox": 0.18275862068965518, "oy": 0.5137931034482759, "term": "small", "cat25k": 44, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 5, "s": 0.7827586206896552, "os": 0.07065342876933733, "bg": 1.535620205496792e-07}, {"x": 0.6827586206896552, "y": 0.5172413793103449, "ox": 0.6827586206896552, "oy": 0.5172413793103449, "term": "group", "cat25k": 44, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 14, "s": 0.1620689655172414, "os": -0.07688755483722004, "bg": 1.5534898848886986e-07}, {"x": 0.4517241379310345, "y": 0.5206896551724138, "ox": 0.4517241379310345, "oy": 0.5206896551724138, "term": "though", "cat25k": 44, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 8, "s": 0.593103448275862, "os": 0.021473100900484876, "bg": 4.13408018755669e-07}, {"x": 0.9793103448275862, "y": 0.993103448275862, "ox": 0.9793103448275862, "oy": 0.993103448275862, "term": "zoom", "cat25k": 893, "ncat25k": 536, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 225, "ncat": 111, "s": 0.7793103448275862, "os": 0.07019164165319791, "bg": 2.1410185704686634e-05}, {"x": 0.6862068965517242, "y": 0.35517241379310344, "ox": 0.6862068965517242, "oy": 0.35517241379310344, "term": "assignments", "cat25k": 32, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 14, "s": 0.0793103448275862, "os": -0.1191410759639806, "bg": 4.273731325858124e-06}, {"x": 0.8689655172413793, "y": 0.9344827586206896, "ox": 0.8689655172413793, "oy": 0.9344827586206896, "term": "has", "cat25k": 254, "ncat25k": 154, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 64, "ncat": 32, "s": 0.9689655172413794, "os": 0.2241976448857077, "bg": 1.8349797984254624e-07}, {"x": 0.996551724137931, "y": 0.9862068965517241, "ox": 0.996551724137931, "oy": 0.9862068965517241, "term": "to", "cat25k": 715, "ncat25k": 912, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 180, "ncat": 189, "s": 0.2896551724137931, "os": -0.03994458554606328, "bg": 6.080582954274185e-08}, {"x": 0.5172413793103449, "y": 0.593103448275862, "ox": 0.5172413793103449, "oy": 0.593103448275862, "term": "effective", "cat25k": 52, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 9, "s": 0.6517241379310345, "os": 0.0332486723620411, "bg": 5.791469531295975e-07}, {"x": 0.10344827586206896, "y": 0.15862068965517243, "ox": 0.10344827586206896, "oy": 0.15862068965517243, "term": "access", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 8.256882324720447e-08}, {"x": 0.6241379310344828, "y": 0.7620689655172413, "ox": 0.6241379310344828, "oy": 0.7620689655172413, "term": "/", "cat25k": 87, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 22, "ncat": 12, "s": 0.8689655172413794, "os": 0.11082890787347036, "bg": 0.0}, {"x": 0.5862068965517241, "y": 0.7241379310344828, "ox": 0.5862068965517241, "oy": 0.7241379310344828, "term": "professor", "cat25k": 75, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 19, "ncat": 11, "s": 0.8310344827586206, "os": 0.0849688293696606, "bg": 1.4783557264392414e-06}, {"x": 0.02413793103448276, "y": 0.27241379310344827, "ox": 0.02413793103448276, "oy": 0.27241379310344827, "term": "activities", "cat25k": 28, "ncat25k": 10, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 2, "s": 0.7551724137931034, "os": 0.06349572846917571, "bg": 1.3564618723737578e-07}, {"x": 0.2689655172413793, "y": 0.7517241379310344, "ox": 0.2689655172413793, "oy": 0.7517241379310344, "term": "good", "cat25k": 83, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 21, "ncat": 6, "s": 0.9413793103448276, "os": 0.1951050565689217, "bg": 1.4761786266677223e-07}, {"x": 0.9310344827586207, "y": 0.9586206896551724, "ox": 0.9310344827586207, "oy": 0.9586206896551724, "term": "been", "cat25k": 341, "ncat25k": 265, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 86, "ncat": 55, "s": 0.8862068965517241, "os": 0.1260678827060725, "bg": 4.904070741825634e-07}, {"x": 0.10689655172413794, "y": 0.27586206896551724, "ox": 0.10689655172413794, "oy": 0.27586206896551724, "term": "about", "cat25k": 28, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 4, "s": 0.6310344827586206, "os": 0.03070884322327408, "bg": 1.7933608415431178e-08}, {"x": 0.7275862068965517, "y": 0.6620689655172414, "ox": 0.7275862068965517, "oy": 0.6620689655172414, "term": "same", "cat25k": 64, "ncat25k": 72, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 15, "s": 0.3896551724137931, "os": -0.022858462248903283, "bg": 2.640145063877693e-07}, {"x": 0.9172413793103448, "y": 0.9413793103448276, "ox": 0.9172413793103448, "oy": 0.9413793103448276, "term": "me", "cat25k": 278, "ncat25k": 212, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 70, "ncat": 44, "s": 0.8620689655172413, "os": 0.10482567536365739, "bg": 4.023784484197023e-07}, {"x": 0.8068965517241379, "y": 0.8689655172413793, "ox": 0.8068965517241379, "oy": 0.8689655172413793, "term": "have been", "cat25k": 159, "ncat25k": 111, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 40, "ncat": 23, "s": 0.9310344827586207, "os": 0.17224659432001854, "bg": 0.0}, {"x": 0.6275862068965518, "y": 0.6517241379310345, "ox": 0.6275862068965518, "oy": 0.6517241379310345, "term": "the same", "cat25k": 60, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 15, "ncat": 12, "s": 0.5448275862068965, "os": 0.0122373585776957, "bg": 0.0}, {"x": 0.8482758620689655, "y": 0.896551724137931, "ox": 0.8482758620689655, "oy": 0.896551724137931, "term": "for me", "cat25k": 179, "ncat25k": 130, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 45, "ncat": 27, "s": 0.9241379310344827, "os": 0.16301085199722926, "bg": 0.0}, {"x": 0.6896551724137931, "y": 0.803448275862069, "ox": 0.6896551724137931, "oy": 0.803448275862069, "term": "fine", "cat25k": 107, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 27, "ncat": 14, "s": 0.9103448275862068, "os": 0.14846455783883628, "bg": 1.139119386532533e-06}, {"x": 0.18620689655172415, "y": 0.3586206896551724, "ox": 0.18620689655172415, "oy": 0.3586206896551724, "term": "been fine", "cat25k": 32, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 5, "s": 0.6172413793103448, "os": 0.02839990764257677, "bg": 0.0}, {"x": 0.1896551724137931, "y": 0.49310344827586206, "ox": 0.1896551724137931, "oy": 0.49310344827586206, "term": "pretty", "cat25k": 40, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 10, "ncat": 5, "s": 0.7379310344827587, "os": 0.056568921727083804, "bg": 5.810117234608854e-07}, {"x": 0.8827586206896552, "y": 0.9137931034482759, "ox": 0.8827586206896552, "oy": 0.9137931034482759, "term": "well", "cat25k": 218, "ncat25k": 159, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 55, "ncat": 33, "s": 0.9137931034482758, "os": 0.15146617409374274, "bg": 4.860592034249676e-07}, {"x": 0.9, "y": 0.5241379310344828, "ox": 0.9, "oy": 0.5241379310344828, "term": "just", "cat25k": 44, "ncat25k": 188, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 39, "s": 0.0, "os": -0.42114984991918725, "bg": 2.1605309776240204e-07}, {"x": 0.45517241379310347, "y": 0.3620689655172414, "ox": 0.45517241379310347, "oy": 0.3620689655172414, "term": "does", "cat25k": 32, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 8, "s": 0.3931034482758621, "os": -0.020780420226275687, "bg": 1.0190051238348047e-07}, {"x": 0.9620689655172414, "y": 0.8655172413793103, "ox": 0.9620689655172414, "oy": 0.8655172413793103, "term": "not", "cat25k": 151, "ncat25k": 396, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 38, "ncat": 82, "s": 0.013793103448275864, "os": -0.28446086354190725, "bg": 9.113346474419478e-08}, {"x": 0.5896551724137931, "y": 0.7275862068965517, "ox": 0.5896551724137931, "oy": 0.7275862068965517, "term": "feel", "cat25k": 75, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 19, "ncat": 11, "s": 0.8310344827586206, "os": 0.0849688293696606, "bg": 6.526208448229047e-07}, {"x": 0.593103448275862, "y": 0.696551724137931, "ox": 0.593103448275862, "oy": 0.696551724137931, "term": "having", "cat25k": 67, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 17, "ncat": 11, "s": 0.7413793103448276, "os": 0.05679981528515354, "bg": 5.120089458203014e-07}, {"x": 0.19310344827586207, "y": 0.20689655172413793, "ox": 0.19310344827586207, "oy": 0.20689655172413793, "term": "learn", "cat25k": 24, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 5, "s": 0.4689655172413793, "os": 0.00023089355806972522, "bg": 1.2260279355369225e-07}, {"x": 0.3689655172413793, "y": 0.42758620689655175, "ox": 0.3689655172413793, "oy": 0.42758620689655175, "term": "through", "cat25k": 36, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 7, "s": 0.5137931034482758, "os": 0.009697529438928654, "bg": 9.346168785195847e-08}, {"x": 0.27241379310344827, "y": 0.2103448275862069, "ox": 0.27241379310344827, "oy": 0.2103448275862069, "term": "screen", "cat25k": 24, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 6, "s": 0.4103448275862069, "os": -0.0161625490648811, "bg": 3.108935547102705e-07}, {"x": 0.8620689655172413, "y": 0.7965517241379311, "ox": 0.8620689655172413, "oy": 0.7965517241379311, "term": "very", "cat25k": 103, "ncat25k": 150, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 26, "ncat": 31, "s": 0.0896551724137931, "os": -0.11152158854767952, "bg": 3.403631358181176e-07}, {"x": 0.9137931034482759, "y": 0.903448275862069, "ox": 0.9137931034482759, "oy": 0.903448275862069, "term": "on", "cat25k": 187, "ncat25k": 207, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 47, "ncat": 43, "s": 0.4413793103448276, "os": -0.005541445393673516, "bg": 4.799441659834167e-08}, {"x": 0.027586206896551724, "y": 0.596551724137931, "ox": 0.027586206896551724, "oy": 0.596551724137931, "term": "great", "cat25k": 52, "ncat25k": 10, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 2, "s": 0.9, "os": 0.14800277072269682, "bg": 9.950235225219096e-08}, {"x": 0.596551724137931, "y": 0.5275862068965518, "ox": 0.596551724137931, "oy": 0.5275862068965518, "term": "worked well", "cat25k": 44, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 11, "s": 0.3758620689655172, "os": -0.027707226968367582, "bg": 0.0}, {"x": 0.27586206896551724, "y": 0.43103448275862066, "ox": 0.27586206896551724, "oy": 0.43103448275862066, "term": "especially", "cat25k": 36, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 6, "s": 0.6068965517241379, "os": 0.026090972061879478, "bg": 5.054814407434217e-07}, {"x": 0.7310344827586207, "y": 0.7379310344827587, "ox": 0.7310344827586207, "oy": 0.7379310344827587, "term": "pre", "cat25k": 79, "ncat25k": 72, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 20, "ncat": 15, "s": 0.6586206896551724, "os": 0.03347956592011081, "bg": 9.880707396542287e-07}, {"x": 0.7655172413793103, "y": 0.7655172413793103, "ox": 0.7655172413793103, "oy": 0.7655172413793103, "term": "-", "cat25k": 87, "ncat25k": 87, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 22, "ncat": 18, "s": 0.5551724137931034, "os": 0.012468252135765412, "bg": 0.0}, {"x": 0.6931034482758621, "y": 0.7310344827586207, "ox": 0.6931034482758621, "oy": 0.7310344827586207, "term": "pre -", "cat25k": 75, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 19, "ncat": 14, "s": 0.6655172413793103, "os": 0.035788501500808145, "bg": 0.0}, {"x": 0.5206896551724138, "y": 0.07586206896551724, "ox": 0.5206896551724138, "oy": 0.07586206896551724, "term": "attention", "cat25k": 16, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 9, "s": 0.11724137931034483, "os": -0.09351189101824058, "bg": 5.808046736011767e-07}, {"x": 0.6, "y": 0.6, "ox": 0.6, "oy": 0.6, "term": "over", "cat25k": 52, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 11, "s": 0.4724137931034483, "os": 0.00046178711613945045, "bg": 1.0452145804193802e-07}, {"x": 0.696551724137931, "y": 0.43448275862068964, "ox": 0.696551724137931, "oy": 0.43448275862068964, "term": "was", "cat25k": 36, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 14, "s": 0.09999999999999999, "os": -0.10505656892172707, "bg": 3.100897126884395e-08}, {"x": 0.19655172413793104, "y": 0.7827586206896552, "ox": 0.19655172413793104, "oy": 0.7827586206896552, "term": "helpful", "cat25k": 95, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 24, "ncat": 5, "s": 0.9793103448275862, "os": 0.2537520203186331, "bg": 1.254821027797509e-06}, {"x": 0.05172413793103448, "y": 0.21379310344827587, "ox": 0.05172413793103448, "oy": 0.21379310344827587, "term": "too", "cat25k": 24, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 3, "s": 0.6413793103448275, "os": 0.03301777880397136, "bg": 1.0221103536320682e-07}, {"x": 0.2, "y": 0.4379310344827586, "ox": 0.2, "oy": 0.4379310344827586, "term": "these", "cat25k": 36, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 5, "s": 0.6827586206896552, "os": 0.0424844146848303, "bg": 5.175438483156908e-08}, {"x": 0.9482758620689655, "y": 0.9275862068965517, "ox": 0.9482758620689655, "oy": 0.9275862068965517, "term": "that", "cat25k": 230, "ncat25k": 352, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 58, "ncat": 73, "s": 0.18620689655172415, "os": -0.06626645116601249, "bg": 7.705782180039241e-08}, {"x": 0.3724137931034483, "y": 0.02413793103448276, "ox": 0.3724137931034483, "oy": 0.02413793103448276, "term": "doing", "cat25k": 12, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 7, "s": 0.16896551724137931, "os": -0.07480951281459247, "bg": 2.474178208202863e-07}, {"x": 0.8551724137931035, "y": 0.8724137931034482, "ox": 0.8551724137931035, "oy": 0.8724137931034482, "term": "work", "cat25k": 163, "ncat25k": 145, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 41, "ncat": 30, "s": 0.8413793103448276, "os": 0.08797044562456713, "bg": 3.3850064581155606e-07}, {"x": 0.903448275862069, "y": 0.9206896551724137, "ox": 0.903448275862069, "oy": 0.9206896551724137, "term": "but", "cat25k": 226, "ncat25k": 193, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 57, "ncat": 40, "s": 0.8172413793103448, "os": 0.08358346802124217, "bg": 1.9401693457411735e-07}, {"x": 0.4586206896551724, "y": 0.8137931034482758, "ox": 0.4586206896551724, "oy": 0.8137931034482758, "term": "live", "cat25k": 115, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 29, "ncat": 8, "s": 0.9862068965517241, "os": 0.27499422766104825, "bg": 4.457347166103904e-07}, {"x": 0.6310344827586207, "y": 0.7, "ox": 0.6310344827586207, "oy": 0.7, "term": "office", "cat25k": 67, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 17, "ncat": 12, "s": 0.6793103448275862, "os": 0.04040637266220273, "bg": 2.1738917282580165e-07}, {"x": 0.7344827586206897, "y": 0.7551724137931034, "ox": 0.7344827586206897, "oy": 0.7551724137931034, "term": "hours", "cat25k": 83, "ncat25k": 72, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 21, "ncat": 15, "s": 0.7275862068965517, "os": 0.04756407296236431, "bg": 3.631669886453067e-07}, {"x": 0.2793103448275862, "y": 0.7862068965517242, "ox": 0.2793103448275862, "oy": 0.7862068965517242, "term": "most", "cat25k": 95, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 24, "ncat": 6, "s": 0.9724137931034482, "os": 0.23735857769568225, "bg": 1.4415335402834121e-07}, {"x": 0.5517241379310345, "y": 0.6655172413793103, "ox": 0.5517241379310345, "oy": 0.6655172413793103, "term": "office hours", "cat25k": 64, "ncat25k": 48, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 10, "s": 0.7448275862068966, "os": 0.05910875086585082, "bg": 0.0}, {"x": 0.9344827586206896, "y": 0.7689655172413793, "ox": 0.9344827586206896, "oy": 0.7689655172413793, "term": "n't", "cat25k": 87, "ncat25k": 265, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 22, "ncat": 55, "s": 0.006896551724137931, "os": -0.38097437081505425, "bg": 0.0}, {"x": 0.9206896551724137, "y": 0.8758620689655172, "ox": 0.9206896551724137, "oy": 0.8758620689655172, "term": "as", "cat25k": 163, "ncat25k": 212, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 41, "ncat": 44, "s": 0.1310344827586207, "os": -0.09235742322789187, "bg": 7.564145769293848e-08}, {"x": 0.3758620689655172, "y": 0.2793103448275862, "ox": 0.3758620689655172, "oy": 0.2793103448275862, "term": "now", "cat25k": 28, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 7, "s": 0.396551724137931, "os": -0.018471484645578393, "bg": 4.5796478991687145e-08}, {"x": 0.8344827586206897, "y": 0.7413793103448276, "ox": 0.8344827586206897, "oy": 0.7413793103448276, "term": "we", "cat25k": 79, "ncat25k": 121, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 20, "ncat": 25, "s": 0.08275862068965517, "os": -0.11406141768644656, "bg": 6.471677785816863e-08}, {"x": 0.1103448275862069, "y": 0.16206896551724137, "ox": 0.1103448275862069, "oy": 0.16206896551724137, "term": "ca", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 1.3810143048300444e-07}, {"x": 0.9655172413793104, "y": 0.9448275862068966, "ox": 0.9655172413793104, "oy": 0.9448275862068966, "term": "in", "cat25k": 290, "ncat25k": 405, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 73, "ncat": 84, "s": 0.19310344827586207, "os": -0.061417686446548214, "bg": 3.707456599167326e-08}, {"x": 0.3793103448275862, "y": 0.36551724137931035, "ox": 0.3793103448275862, "oy": 0.36551724137931035, "term": "courses", "cat25k": 32, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 7, "s": 0.44482758620689655, "os": -0.004386977603324876, "bg": 4.4283909695306624e-07}, {"x": 0.7, "y": 0.21724137931034482, "ox": 0.7, "oy": 0.21724137931034482, "term": "any", "cat25k": 24, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 14, "s": 0.06206896551724138, "os": -0.14731009004848766, "bg": 5.62782402274897e-08}, {"x": 0.03103448275862069, "y": 0.3689655172413793, "ox": 0.03103448275862069, "oy": 0.3689655172413793, "term": "others", "cat25k": 32, "ncat25k": 10, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 2, "s": 0.793103448275862, "os": 0.07758023551142923, "bg": 1.795159888114506e-07}, {"x": 0.5241379310344828, "y": 0.2827586206896552, "ox": 0.5241379310344828, "oy": 0.2827586206896552, "term": "our", "cat25k": 28, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 9, "s": 0.24482758620689657, "os": -0.05125836989148001, "bg": 3.203937758050341e-08}, {"x": 0.7862068965517242, "y": 0.8862068965517241, "ox": 0.7862068965517242, "oy": 0.8862068965517241, "term": "time", "cat25k": 175, "ncat25k": 101, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 44, "ncat": 21, "s": 0.9758620689655172, "os": 0.24728700069268067, "bg": 1.4305858821421725e-07}, {"x": 0.2827586206896552, "y": 0.07931034482758621, "ox": 0.2827586206896552, "oy": 0.07931034482758621, "term": "myself", "cat25k": 16, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 6, "s": 0.2724137931034483, "os": -0.04433156314938813, "bg": 5.263625526309916e-07}, {"x": 0.8379310344827586, "y": 0.6689655172413793, "ox": 0.8379310344827586, "oy": 0.6689655172413793, "term": "or", "cat25k": 64, "ncat25k": 121, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 25, "s": 0.03793103448275862, "os": -0.17039944585546066, "bg": 3.165103070560554e-08}, {"x": 0.8724137931034482, "y": 0.7724137931034483, "ox": 0.8724137931034482, "oy": 0.7724137931034483, "term": "at", "cat25k": 87, "ncat25k": 154, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 22, "ncat": 32, "s": 0.03448275862068965, "os": -0.18425305933964442, "bg": 4.7529232646598895e-08}, {"x": 0.7896551724137931, "y": 0.7448275862068966, "ox": 0.7896551724137931, "oy": 0.7448275862068966, "term": "this", "cat25k": 79, "ncat25k": 101, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 20, "ncat": 21, "s": 0.2620689655172414, "os": -0.04848764719464327, "bg": 2.5398927503710203e-08}, {"x": 0.7689655172413793, "y": 0.7034482758620689, "ox": 0.7689655172413793, "oy": 0.7034482758620689, "term": "so", "cat25k": 67, "ncat25k": 87, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 17, "ncat": 18, "s": 0.23793103448275862, "os": -0.05795428307550221, "bg": 1.0576853122953156e-07}, {"x": 0.20344827586206896, "y": 0.5827586206896552, "ox": 0.20344827586206896, "oy": 0.5827586206896552, "term": "being", "cat25k": 48, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 12, "ncat": 5, "s": 0.8206896551724138, "os": 0.08473793581159086, "bg": 1.4003521383148569e-07}, {"x": 0.28620689655172415, "y": 0.4413793103448276, "ox": 0.28620689655172415, "oy": 0.4413793103448276, "term": "able", "cat25k": 36, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 6, "s": 0.6068965517241379, "os": 0.026090972061879478, "bg": 2.7421797649107354e-07}, {"x": 0.2896551724137931, "y": 0.603448275862069, "ox": 0.2896551724137931, "oy": 0.603448275862069, "term": "own", "cat25k": 52, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 6, "s": 0.8103448275862069, "os": 0.08242900023089354, "bg": 1.637756620461975e-07}, {"x": 0.20689655172413793, "y": 0.44482758620689655, "ox": 0.20689655172413793, "oy": 0.44482758620689655, "term": "able to", "cat25k": 36, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 5, "s": 0.6827586206896552, "os": 0.0424844146848303, "bg": 0.0}, {"x": 0.7034482758620689, "y": 0.8517241379310345, "ox": 0.7034482758620689, "oy": 0.8517241379310345, "term": "has been", "cat25k": 139, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 35, "ncat": 14, "s": 0.9827586206896551, "os": 0.26114061417686446, "bg": 0.0}, {"x": 0.7413793103448276, "y": 0.496551724137931, "ox": 0.7413793103448276, "oy": 0.496551724137931, "term": "there", "cat25k": 40, "ncat25k": 77, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 10, "ncat": 16, "s": 0.07586206896551724, "os": -0.12375894712537519, "bg": 7.416036250817398e-08}, {"x": 0.7724137931034483, "y": 0.7103448275862069, "ox": 0.7724137931034483, "oy": 0.7103448275862069, "term": "much", "cat25k": 71, "ncat25k": 87, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 18, "ncat": 18, "s": 0.2827586206896552, "os": -0.04386977603324871, "bg": 2.971041003374026e-07}, {"x": 0.46206896551724136, "y": 0.4482758620689655, "ox": 0.46206896551724136, "oy": 0.4482758620689655, "term": "make", "cat25k": 36, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 8, "s": 0.4344827586206897, "os": -0.006695913184022156, "bg": 8.393038612341997e-08}, {"x": 0.5551724137931034, "y": 0.5310344827586206, "ox": 0.5551724137931034, "oy": 0.5310344827586206, "term": "readings", "cat25k": 44, "ncat25k": 48, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 10, "s": 0.4241379310344828, "os": -0.011313784345416772, "bg": 4.832217915539964e-06}, {"x": 0.29310344827586204, "y": 0.28620689655172415, "ox": 0.29310344827586204, "oy": 0.28620689655172415, "term": "posted", "cat25k": 28, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 6, "s": 0.4551724137931034, "os": -0.0020780420226275687, "bg": 9.85355158950104e-08}, {"x": 0.013793103448275862, "y": 0.5, "ox": 0.013793103448275862, "oy": 0.5, "term": "schedule", "cat25k": 40, "ncat25k": 5, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 10, "ncat": 1, "s": 0.8793103448275862, "os": 0.12214269221888707, "bg": 3.4099280147146455e-07}, {"x": 0.9689655172413794, "y": 0.9689655172413794, "ox": 0.9689655172413794, "oy": 0.9689655172413794, "term": "is", "cat25k": 405, "ncat25k": 415, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 102, "ncat": 86, "s": 0.5896551724137932, "os": 0.020780420226275687, "bg": 7.990212891931436e-08}, {"x": 0.296551724137931, "y": 0.3724137931034483, "ox": 0.296551724137931, "oy": 0.3724137931034483, "term": "different", "cat25k": 32, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 6, "s": 0.5344827586206896, "os": 0.012006465019625948, "bg": 1.5572234889833642e-07}, {"x": 0.6586206896551724, "y": 0.6068965517241379, "ox": 0.6586206896551724, "oy": 0.6068965517241379, "term": "than", "cat25k": 52, "ncat25k": 63, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 13, "s": 0.3241379310344828, "os": -0.0323250981297622, "bg": 1.0345741428017039e-07}, {"x": 0.46551724137931033, "y": 0.2206896551724138, "ox": 0.46551724137931033, "oy": 0.2206896551724138, "term": "what", "cat25k": 24, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 8, "s": 0.2517241379310345, "os": -0.04894943431078273, "bg": 3.446541721019604e-08}, {"x": 0.05517241379310345, "y": 0.2896551724137931, "ox": 0.05517241379310345, "oy": 0.2896551724137931, "term": "my own", "cat25k": 28, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 3, "s": 0.706896551724138, "os": 0.04710228584622489, "bg": 0.0}, {"x": 0.8103448275862069, "y": 0.8793103448275862, "ox": 0.8103448275862069, "oy": 0.8793103448275862, "term": "asynchronous", "cat25k": 163, "ncat25k": 111, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 41, "ncat": 23, "s": 0.9379310344827586, "os": 0.18633110136227204, "bg": 5.8638774156426264e-05}, {"x": 0.7448275862068966, "y": 0.29310344827586204, "ox": 0.7448275862068966, "oy": 0.29310344827586204, "term": "would", "cat25k": 28, "ncat25k": 77, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 16, "s": 0.044827586206896544, "os": -0.16601246825213573, "bg": 8.032729741505798e-08}, {"x": 0.11379310344827587, "y": 0.22413793103448276, "ox": 0.11379310344827587, "oy": 0.22413793103448276, "term": "always", "cat25k": 24, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 4, "s": 0.5724137931034482, "os": 0.01662433618102055, "bg": 1.566811890804931e-07}, {"x": 0.6620689655172414, "y": 0.6724137931034483, "ox": 0.6620689655172414, "oy": 0.6724137931034483, "term": "if", "cat25k": 64, "ncat25k": 63, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 13, "s": 0.5206896551724138, "os": 0.009928422996998365, "bg": 5.110128102004036e-08}, {"x": 0.11724137931034483, "y": 0.8413793103448276, "ox": 0.11724137931034483, "oy": 0.8413793103448276, "term": "both", "cat25k": 131, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 33, "ncat": 4, "s": 0.996551724137931, "os": 0.3969060263218656, "bg": 3.236224116619383e-07}, {"x": 0.3, "y": 0.5344827586206896, "ox": 0.3, "oy": 0.5344827586206896, "term": "get", "cat25k": 44, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 6, "s": 0.7310344827586206, "os": 0.05425998614638651, "bg": 5.610584294664323e-08}, {"x": 0.603448275862069, "y": 0.5379310344827586, "ox": 0.603448275862069, "oy": 0.5379310344827586, "term": "up", "cat25k": 44, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 11, "s": 0.3758620689655172, "os": -0.027707226968367582, "bg": 5.301317481854292e-08}, {"x": 0.2103448275862069, "y": 0.4517241379310345, "ox": 0.2103448275862069, "oy": 0.4517241379310345, "term": "attend", "cat25k": 36, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 5, "s": 0.6827586206896552, "os": 0.0424844146848303, "bg": 1.3557593358677317e-06}, {"x": 0.05862068965517241, "y": 0.296551724137931, "ox": 0.05862068965517241, "oy": 0.296551724137931, "term": "to attend", "cat25k": 28, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 3, "s": 0.706896551724138, "os": 0.04710228584622489, "bg": 0.0}, {"x": 0.034482758620689655, "y": 0.6103448275862069, "ox": 0.034482758620689655, "oy": 0.6103448275862069, "term": "has worked", "cat25k": 52, "ncat25k": 10, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 2, "s": 0.9, "os": 0.14800277072269682, "bg": 0.0}, {"x": 0.006896551724137931, "y": 0.6758620689655173, "ox": 0.006896551724137931, "oy": 0.6758620689655173, "term": "nice", "cat25k": 64, "ncat25k": 0, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 0, "s": 0.9655172413793104, "os": 0.22304317709535904, "bg": 4.6103803578202637e-07}, {"x": 0.8448275862068966, "y": 0.8241379310344827, "ox": 0.8448275862068966, "oy": 0.8241379310344827, "term": "learning", "cat25k": 119, "ncat25k": 125, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 30, "ncat": 26, "s": 0.5275862068965518, "os": 0.010390210113137843, "bg": 9.516860758793245e-07}, {"x": 0.38275862068965516, "y": 0.3, "ox": 0.38275862068965516, "oy": 0.3, "term": "asynchronous learning", "cat25k": 28, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 7, "s": 0.396551724137931, "os": -0.018471484645578393, "bg": 0.0}, {"x": 0.6068965517241379, "y": 0.6793103448275862, "ox": 0.6068965517241379, "oy": 0.6793103448275862, "term": "some", "cat25k": 64, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 11, "s": 0.696551724137931, "os": 0.04271530824290001, "bg": 9.838889173670071e-08}, {"x": 0.8586206896551725, "y": 0.6137931034482759, "ox": 0.8586206896551725, "oy": 0.6137931034482759, "term": "hard", "cat25k": 52, "ncat25k": 145, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 30, "s": 0.017241379310344827, "os": -0.2782267374740245, "bg": 6.611940506435893e-07}, {"x": 0.21379310344827587, "y": 0.08275862068965517, "ox": 0.21379310344827587, "oy": 0.08275862068965517, "term": "internet", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 6.82360402452981e-08}, {"x": 0.21724137931034482, "y": 0.08620689655172414, "ox": 0.21724137931034482, "oy": 0.08620689655172414, "term": "connection", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 2.9356395761334397e-07}, {"x": 0.7068965517241379, "y": 0.8344827586206897, "ox": 0.7068965517241379, "oy": 0.8344827586206897, "term": "meetings", "cat25k": 127, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 32, "ncat": 14, "s": 0.9620689655172414, "os": 0.2188870930501039, "bg": 2.3397372790391533e-06}, {"x": 0.38620689655172413, "y": 0.3758620689655172, "ox": 0.38620689655172413, "oy": 0.3758620689655172, "term": "see", "cat25k": 32, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 7, "s": 0.44482758620689655, "os": -0.004386977603324876, "bg": 4.402549393082151e-08}, {"x": 0.4689655172413793, "y": 0.7482758620689656, "ox": 0.4689655172413793, "oy": 0.7482758620689656, "term": "videos", "cat25k": 79, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 20, "ncat": 8, "s": 0.906896551724138, "os": 0.14823366428076656, "bg": 5.952247710101216e-07}, {"x": 0.4724137931034483, "y": 0.22758620689655173, "ox": 0.4724137931034483, "oy": 0.22758620689655173, "term": "forums", "cat25k": 24, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 8, "s": 0.2517241379310345, "os": -0.04894943431078273, "bg": 1.7674131731767478e-07}, {"x": 0.30344827586206896, "y": 0.5413793103448276, "ox": 0.30344827586206896, "oy": 0.5413793103448276, "term": "watch", "cat25k": 44, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 6, "s": 0.7310344827586206, "os": 0.05425998614638651, "bg": 3.6948508732106273e-07}, {"x": 0.2206896551724138, "y": 0.16551724137931034, "ox": 0.2206896551724138, "oy": 0.16551724137931034, "term": "to watch", "cat25k": 20, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 5, "s": 0.4206896551724138, "os": -0.013853613484183791, "bg": 0.0}, {"x": 0.5275862068965518, "y": 0.3793103448275862, "ox": 0.5275862068965518, "oy": 0.3793103448275862, "term": "had", "cat25k": 32, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 9, "s": 0.3, "os": -0.0371738628492265, "bg": 7.079709230178406e-08}, {"x": 0.5310344827586206, "y": 0.30344827586206896, "ox": 0.5310344827586206, "oy": 0.30344827586206896, "term": "their", "cat25k": 28, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 9, "s": 0.24482758620689657, "os": -0.05125836989148001, "bg": 4.0875638333128667e-08}, {"x": 0.06206896551724138, "y": 0.45517241379310347, "ox": 0.06206896551724138, "oy": 0.45517241379310347, "term": "prefer", "cat25k": 36, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 3, "s": 0.7896551724137931, "os": 0.07527129993073194, "bg": 1.4982551881924006e-06}, {"x": 0.6655172413793103, "y": 0.6172413793103448, "ox": 0.6655172413793103, "oy": 0.6172413793103448, "term": "find", "cat25k": 52, "ncat25k": 63, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 13, "s": 0.3241379310344828, "os": -0.0323250981297622, "bg": 1.0357409730458591e-07}, {"x": 0.010344827586206896, "y": 0.4586206896551724, "ox": 0.010344827586206896, "oy": 0.4586206896551724, "term": "go", "cat25k": 36, "ncat25k": 0, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 0, "s": 0.8827586206896552, "os": 0.1244516277995844, "bg": 4.2745258973718814e-08}, {"x": 0.47586206896551725, "y": 0.027586206896551724, "ox": 0.47586206896551725, "oy": 0.027586206896551724, "term": "material", "cat25k": 12, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 8, "s": 0.13448275862068967, "os": -0.09120295543754328, "bg": 2.2325665826957785e-07}, {"x": 0.017241379310344827, "y": 0.38275862068965516, "ox": 0.017241379310344827, "oy": 0.38275862068965516, "term": "i prefer", "cat25k": 32, "ncat25k": 5, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 1, "s": 0.8482758620689655, "os": 0.09397367813438004, "bg": 0.0}, {"x": 0.8862068965517241, "y": 0.8896551724137931, "ox": 0.8862068965517241, "oy": 0.8896551724137931, "term": "synchronous", "cat25k": 175, "ncat25k": 159, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 44, "ncat": 33, "s": 0.7689655172413793, "os": 0.06695913184022162, "bg": 7.931994989451476e-05}, {"x": 0.1206896551724138, "y": 0.503448275862069, "ox": 0.1206896551724138, "oy": 0.503448275862069, "term": "better", "cat25k": 40, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 10, "ncat": 4, "s": 0.7862068965517242, "os": 0.07296236435003463, "bg": 1.7823909790849974e-07}, {"x": 0.3896551724137931, "y": 0.0896551724137931, "ox": 0.3896551724137931, "oy": 0.0896551724137931, "term": "microsoft", "cat25k": 16, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 7, "s": 0.19655172413793104, "os": -0.060725005772338955, "bg": 2.1532200877895233e-07}, {"x": 0.5344827586206896, "y": 0.09310344827586207, "ox": 0.5344827586206896, "oy": 0.09310344827586207, "term": "teams", "cat25k": 16, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 9, "s": 0.11724137931034483, "os": -0.09351189101824058, "bg": 7.558960033626906e-07}, {"x": 0.30689655172413793, "y": 0.03103448275862069, "ox": 0.30689655172413793, "oy": 0.03103448275862069, "term": "microsoft teams", "cat25k": 12, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 6, "s": 0.21379310344827587, "os": -0.058416070191641654, "bg": 0.0}, {"x": 0.5379310344827586, "y": 0.38620689655172413, "ox": 0.5379310344827586, "oy": 0.38620689655172413, "term": "need", "cat25k": 32, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 9, "s": 0.3, "os": -0.0371738628492265, "bg": 1.064529545538498e-07}, {"x": 0.12413793103448276, "y": 0.16896551724137931, "ox": 0.12413793103448276, "oy": 0.16896551724137931, "term": "ask", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 1.6915196797930695e-07}, {"x": 0.4793103448275862, "y": 0.5448275862068965, "ox": 0.4793103448275862, "oy": 0.5448275862068965, "term": "questions", "cat25k": 44, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 8, "s": 0.593103448275862, "os": 0.021473100900484876, "bg": 2.4247576020872725e-07}, {"x": 0.12758620689655173, "y": 0.3896551724137931, "ox": 0.12758620689655173, "oy": 0.3896551724137931, "term": "real", "cat25k": 32, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 4, "s": 0.7034482758620689, "os": 0.044793350265527596, "bg": 8.062146518965007e-08}, {"x": 0.3931034482758621, "y": 0.1724137931034483, "ox": 0.3931034482758621, "oy": 0.1724137931034483, "term": "need to", "cat25k": 20, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 7, "s": 0.2689655172413793, "os": -0.04664049873008544, "bg": 0.0}, {"x": 0.6344827586206897, "y": 0.6275862068965518, "ox": 0.6344827586206897, "oy": 0.6275862068965518, "term": "other", "cat25k": 56, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 14, "ncat": 12, "s": 0.4586206896551724, "os": -0.0018471484645578296, "bg": 5.314287417777626e-08}, {"x": 0.4827586206896552, "y": 0.30689655172413793, "ox": 0.4827586206896552, "oy": 0.30689655172413793, "term": "where", "cat25k": 28, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 8, "s": 0.3103448275862069, "os": -0.0348649272685292, "bg": 8.322206566271469e-08}, {"x": 0.8931034482758621, "y": 0.8620689655172413, "ox": 0.8931034482758621, "oy": 0.8620689655172413, "term": "they", "cat25k": 143, "ncat25k": 174, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 36, "ncat": 36, "s": 0.30689655172413793, "os": -0.03625028861694757, "bg": 1.6303667528238884e-07}, {"x": 0.8275862068965517, "y": 0.8172413793103448, "ox": 0.8275862068965517, "oy": 0.8172413793103448, "term": "lecture", "cat25k": 115, "ncat25k": 116, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 29, "ncat": 24, "s": 0.6275862068965518, "os": 0.02909258831678596, "bg": 6.551631958984311e-06}, {"x": 0.6689655172413793, "y": 0.7068965517241379, "ox": 0.6689655172413793, "oy": 0.7068965517241379, "term": "- recorded", "cat25k": 67, "ncat25k": 63, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 17, "ncat": 13, "s": 0.603448275862069, "os": 0.024012930039251895, "bg": 0.0}, {"x": 0.39655172413793105, "y": 0.23103448275862068, "ox": 0.39655172413793105, "oy": 0.23103448275862068, "term": "then", "cat25k": 24, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 7, "s": 0.3172413793103448, "os": -0.03255599168783192, "bg": 7.028130272525293e-08}, {"x": 0.22413793103448276, "y": 0.09655172413793103, "ox": 0.22413793103448276, "oy": 0.09655172413793103, "term": "there are", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 0.0}, {"x": 0.4, "y": 0.5482758620689655, "ox": 0.4, "oy": 0.5482758620689655, "term": "'m", "cat25k": 44, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 7, "s": 0.6724137931034482, "os": 0.037866543523435686, "bg": 0.0}, {"x": 0.40344827586206894, "y": 0.5517241379310345, "ox": 0.40344827586206894, "oy": 0.5517241379310345, "term": "i 'm", "cat25k": 44, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 7, "s": 0.6724137931034482, "os": 0.037866543523435686, "bg": 0.0}, {"x": 0.06551724137931035, "y": 0.3103448275862069, "ox": 0.06551724137931035, "oy": 0.3103448275862069, "term": "'re", "cat25k": 28, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 3, "s": 0.706896551724138, "os": 0.04710228584622489, "bg": 0.0}, {"x": 0.7931034482758621, "y": 0.46206896551724136, "ox": 0.7931034482758621, "oy": 0.46206896551724136, "term": "do n't", "cat25k": 36, "ncat25k": 101, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 21, "s": 0.03103448275862069, "os": -0.203417224659432, "bg": 0.0}, {"x": 0.7965517241379311, "y": 0.6827586206896552, "ox": 0.7965517241379311, "oy": 0.6827586206896552, "term": "'s", "cat25k": 64, "ncat25k": 101, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 21, "s": 0.10689655172413792, "os": -0.10482567536365736, "bg": 0.0}, {"x": 0.7586206896551724, "y": 0.7586206896551724, "ox": 0.7586206896551724, "oy": 0.7586206896551724, "term": "also", "cat25k": 83, "ncat25k": 82, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 21, "ncat": 17, "s": 0.5689655172413793, "os": 0.014777187716462692, "bg": 1.2320806334522097e-07}, {"x": 0.6379310344827587, "y": 0.46551724137931033, "ox": 0.6379310344827587, "oy": 0.46551724137931033, "term": "people", "cat25k": 36, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 12, "s": 0.18275862068965518, "os": -0.07226968367582542, "bg": 8.744236782839391e-08}, {"x": 0.7103448275862069, "y": 0.6206896551724138, "ox": 0.7103448275862069, "oy": 0.6206896551724138, "term": "it 's", "cat25k": 52, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 14, "s": 0.25862068965517243, "os": -0.04871854075271301, "bg": 0.0}, {"x": 0.03793103448275862, "y": 0.3137931034482759, "ox": 0.03793103448275862, "oy": 0.3137931034482759, "term": "probably", "cat25k": 28, "ncat25k": 10, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 2, "s": 0.7551724137931034, "os": 0.06349572846917571, "bg": 2.920197333957174e-07}, {"x": 0.06896551724137931, "y": 0.3931034482758621, "ox": 0.06896551724137931, "oy": 0.3931034482758621, "term": "boards", "cat25k": 32, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 3, "s": 0.7482758620689656, "os": 0.061186792888478406, "bg": 4.1595413251092394e-07}, {"x": 0.07241379310344828, "y": 0.31724137931034485, "ox": 0.07241379310344828, "oy": 0.31724137931034485, "term": "discussion boards", "cat25k": 28, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 3, "s": 0.706896551724138, "os": 0.04710228584622489, "bg": 0.0}, {"x": 0.07586206896551724, "y": 0.23448275862068965, "ox": 0.07586206896551724, "oy": 0.23448275862068965, "term": "smaller", "cat25k": 24, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 3, "s": 0.6413793103448275, "os": 0.03301777880397136, "bg": 7.201289895046001e-07}, {"x": 0.4068965517241379, "y": 0.23793103448275862, "ox": 0.4068965517241379, "oy": 0.23793103448275862, "term": "focus", "cat25k": 24, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 7, "s": 0.3172413793103448, "os": -0.03255599168783192, "bg": 3.9610168905377557e-07}, {"x": 0.020689655172413793, "y": 0.4689655172413793, "ox": 0.020689655172413793, "oy": 0.4689655172413793, "term": "definitely", "cat25k": 36, "ncat25k": 5, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 1, "s": 0.8655172413793104, "os": 0.10805818517663357, "bg": 1.2550805661317012e-06}, {"x": 0.4103448275862069, "y": 0.034482758620689655, "ox": 0.4103448275862069, "oy": 0.034482758620689655, "term": "while", "cat25k": 12, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 7, "s": 0.16896551724137931, "os": -0.07480951281459247, "bg": 8.841421614657019e-08}, {"x": 0.7137931034482758, "y": 0.4724137931034483, "ox": 0.7137931034482758, "oy": 0.4724137931034483, "term": "n\u2019t", "cat25k": 36, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 14, "s": 0.09999999999999999, "os": -0.10505656892172707, "bg": 0.0}, {"x": 0.5413793103448276, "y": 0.1, "ox": 0.5413793103448276, "oy": 0.1, "term": "do n\u2019t", "cat25k": 16, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 9, "s": 0.11724137931034483, "os": -0.09351189101824058, "bg": 0.0}, {"x": 0.41379310344827586, "y": 0.03793103448275862, "ox": 0.41379310344827586, "oy": 0.03793103448275862, "term": "\u2019s", "cat25k": 12, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 7, "s": 0.16896551724137931, "os": -0.07480951281459247, "bg": 0.0}, {"x": 0.8896551724137931, "y": 0.506896551724138, "ox": 0.8896551724137931, "oy": 0.506896551724138, "term": "difficult", "cat25k": 40, "ncat25k": 169, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 10, "ncat": 35, "s": 0.0034482758620689655, "os": -0.38605402909258835, "bg": 2.1201752555712256e-06}, {"x": 0.8137931034482758, "y": 0.10344827586206896, "ox": 0.8137931034482758, "oy": 0.10344827586206896, "term": "difficult to", "cat25k": 16, "ncat25k": 111, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 23, "s": 0.010344827586206896, "os": -0.3066266451166012, "bg": 0.0}, {"x": 0.041379310344827586, "y": 0.39655172413793105, "ox": 0.041379310344827586, "oy": 0.39655172413793105, "term": "structure", "cat25k": 32, "ncat25k": 10, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 2, "s": 0.793103448275862, "os": 0.07758023551142923, "bg": 2.975991545327059e-07}, {"x": 0.07931034482758621, "y": 0.7137931034482758, "ox": 0.07931034482758621, "oy": 0.7137931034482758, "term": "zoom meetings", "cat25k": 71, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 18, "ncat": 3, "s": 0.9482758620689655, "os": 0.20203186331101358, "bg": 0.0}, {"x": 0.5448275862068965, "y": 0.6241379310344828, "ox": 0.5448275862068965, "oy": 0.6241379310344828, "term": "breakout", "cat25k": 52, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 13, "ncat": 9, "s": 0.6517241379310345, "os": 0.0332486723620411, "bg": 2.381586439679828e-05}, {"x": 0.4862068965517241, "y": 0.5551724137931034, "ox": 0.4862068965517241, "oy": 0.5551724137931034, "term": "rooms", "cat25k": 44, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 8, "s": 0.593103448275862, "os": 0.021473100900484876, "bg": 5.804505447963701e-07}, {"x": 0.3103448275862069, "y": 0.4, "ox": 0.3103448275862069, "oy": 0.4, "term": "breakout rooms", "cat25k": 32, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 6, "s": 0.5344827586206896, "os": 0.012006465019625948, "bg": 0.0}, {"x": 0.04482758620689655, "y": 0.40344827586206894, "ox": 0.04482758620689655, "oy": 0.40344827586206894, "term": "each", "cat25k": 32, "ncat25k": 10, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 2, "s": 0.793103448275862, "os": 0.07758023551142923, "bg": 5.86672276661645e-08}, {"x": 0.1310344827586207, "y": 0.32068965517241377, "ox": 0.1310344827586207, "oy": 0.32068965517241377, "term": "method", "cat25k": 28, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 4, "s": 0.6310344827586206, "os": 0.03070884322327408, "bg": 2.606249197986042e-07}, {"x": 0.22758620689655173, "y": 0.10689655172413794, "ox": 0.22758620689655173, "oy": 0.10689655172413794, "term": "its", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 3.424392163399529e-08}, {"x": 0.13448275862068965, "y": 0.32413793103448274, "ox": 0.13448275862068965, "oy": 0.32413793103448274, "term": "course", "cat25k": 28, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 4, "s": 0.6310344827586206, "os": 0.03070884322327408, "bg": 1.2360270790610338e-07}, {"x": 0.7172413793103448, "y": 0.5586206896551724, "ox": 0.7172413793103448, "oy": 0.5586206896551724, "term": "well for", "cat25k": 44, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 14, "s": 0.1620689655172414, "os": -0.07688755483722004, "bg": 0.0}, {"x": 0.8, "y": 0.8551724137931035, "ox": 0.8, "oy": 0.8551724137931035, "term": "think", "cat25k": 139, "ncat25k": 101, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 35, "ncat": 21, "s": 0.9206896551724137, "os": 0.16277995843915954, "bg": 5.140690344499737e-07}, {"x": 0.41724137931034483, "y": 0.1103448275862069, "ox": 0.41724137931034483, "oy": 0.1103448275862069, "term": "even", "cat25k": 16, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 7, "s": 0.19655172413793104, "os": -0.060725005772338955, "bg": 8.953619870576484e-08}, {"x": 0.4206896551724138, "y": 0.47586206896551725, "ox": 0.4206896551724138, "oy": 0.47586206896551725, "term": "i find", "cat25k": 36, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 7, "s": 0.5137931034482758, "os": 0.009697529438928654, "bg": 0.0}, {"x": 0.3137931034482759, "y": 0.2413793103448276, "ox": 0.3137931034482759, "oy": 0.2413793103448276, "term": "haverford", "cat25k": 24, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 6, "s": 0.4103448275862069, "os": -0.0161625490648811, "bg": 6.773461577539202e-05}, {"x": 0.23103448275862068, "y": 0.3275862068965517, "ox": 0.23103448275862068, "oy": 0.3275862068965517, "term": "way", "cat25k": 28, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 5, "s": 0.5586206896551724, "os": 0.014315400600323255, "bg": 7.855238917893576e-08}, {"x": 0.13793103448275862, "y": 0.17586206896551723, "ox": 0.13793103448275862, "oy": 0.17586206896551723, "term": "workload", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 6.342874661272874e-06}, {"x": 0.23448275862068965, "y": 0.11379310344827587, "ox": 0.23448275862068965, "oy": 0.11379310344827587, "term": "engage", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 1.8121548474236092e-06}, {"x": 0.7206896551724138, "y": 0.8206896551724138, "ox": 0.7206896551724138, "oy": 0.8206896551724138, "term": "i think", "cat25k": 115, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 29, "ncat": 14, "s": 0.9344827586206896, "os": 0.17663357192334334, "bg": 0.0}, {"x": 0.23793103448275862, "y": 0.11724137931034483, "ox": 0.23793103448275862, "oy": 0.11724137931034483, "term": "to engage", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 0.0}, {"x": 0.6413793103448275, "y": 0.7344827586206897, "ox": 0.6413793103448275, "oy": 0.7344827586206897, "term": "only", "cat25k": 75, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 19, "ncat": 12, "s": 0.7724137931034483, "os": 0.0685753867467098, "bg": 9.367580866510598e-08}, {"x": 0.7482758620689656, "y": 0.4068965517241379, "ox": 0.7482758620689656, "oy": 0.4068965517241379, "term": "were", "cat25k": 32, "ncat25k": 77, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 16, "s": 0.05517241379310345, "os": -0.15192796120988222, "bg": 8.410538764622604e-08}, {"x": 0.6103448275862069, "y": 0.5620689655172414, "ox": 0.6103448275862069, "oy": 0.5620689655172414, "term": "less", "cat25k": 44, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 11, "s": 0.3758620689655172, "os": -0.027707226968367582, "bg": 3.0252373412140585e-07}, {"x": 0.4896551724137931, "y": 0.3310344827586207, "ox": 0.4896551724137931, "oy": 0.3310344827586207, "term": "everyone", "cat25k": 28, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 8, "s": 0.3103448275862069, "os": -0.0348649272685292, "bg": 4.672101483526154e-07}, {"x": 0.31724137931034485, "y": 0.4793103448275862, "ox": 0.31724137931034485, "oy": 0.4793103448275862, "term": "used", "cat25k": 36, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 6, "s": 0.6068965517241379, "os": 0.026090972061879478, "bg": 7.1182632214105e-08}, {"x": 0.1413793103448276, "y": 0.1793103448275862, "ox": 0.1413793103448276, "oy": 0.1793103448275862, "term": "using", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 6.679980758983422e-08}, {"x": 0.14482758620689656, "y": 0.18275862068965518, "ox": 0.14482758620689656, "oy": 0.18275862068965518, "term": "forum", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 7.072937367901843e-08}, {"x": 0.2413793103448276, "y": 0.1206896551724138, "ox": 0.2413793103448276, "oy": 0.1206896551724138, "term": "everything", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 1.9693426521314736e-07}, {"x": 0.24482758620689654, "y": 0.4827586206896552, "ox": 0.24482758620689654, "oy": 0.4827586206896552, "term": "working", "cat25k": 36, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 5, "s": 0.6827586206896552, "os": 0.0424844146848303, "bg": 1.895876781497012e-07}, {"x": 0.08275862068965517, "y": 0.33448275862068966, "ox": 0.08275862068965517, "oy": 0.33448275862068966, "term": "posts", "cat25k": 28, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 3, "s": 0.706896551724138, "os": 0.04710228584622489, "bg": 9.223598819237308e-08}, {"x": 0.08620689655172414, "y": 0.24482758620689654, "ox": 0.08620689655172414, "oy": 0.24482758620689654, "term": "through zoom", "cat25k": 24, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 3, "s": 0.6413793103448275, "os": 0.03301777880397136, "bg": 0.0}, {"x": 0.0896551724137931, "y": 0.5655172413793104, "ox": 0.0896551724137931, "oy": 0.5655172413793104, "term": "person", "cat25k": 44, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 3, "s": 0.8586206896551724, "os": 0.10344031401523897, "bg": 1.9078452552437006e-07}, {"x": 0.09310344827586207, "y": 0.4103448275862069, "ox": 0.09310344827586207, "oy": 0.4103448275862069, "term": "in person", "cat25k": 32, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 3, "s": 0.7482758620689656, "os": 0.061186792888478406, "bg": 0.0}, {"x": 0.09655172413793103, "y": 0.33793103448275863, "ox": 0.09655172413793103, "oy": 0.33793103448275863, "term": "going", "cat25k": 28, "ncat25k": 14, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 3, "s": 0.706896551724138, "os": 0.04710228584622489, "bg": 1.2878544201121237e-07}, {"x": 0.7241379310344828, "y": 0.6862068965517242, "ox": 0.7241379310344828, "oy": 0.6862068965517242, "term": "am", "cat25k": 64, "ncat25k": 68, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 14, "s": 0.4379310344827586, "os": -0.006465019625952445, "bg": 1.0408549479845058e-07}, {"x": 0.6448275862068965, "y": 0.6551724137931034, "ox": 0.6448275862068965, "oy": 0.6551724137931034, "term": "i am", "cat25k": 60, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 15, "ncat": 12, "s": 0.5448275862068965, "os": 0.0122373585776957, "bg": 0.0}, {"x": 0.32068965517241377, "y": 0.18620689655172415, "ox": 0.32068965517241377, "oy": 0.18620689655172415, "term": "reading", "cat25k": 20, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 6, "s": 0.33448275862068966, "os": -0.030247056107134615, "bg": 2.3084407348501366e-07}, {"x": 0.2482758620689655, "y": 0.3413793103448276, "ox": 0.2482758620689655, "oy": 0.3413793103448276, "term": "week", "cat25k": 28, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 5, "s": 0.5586206896551724, "os": 0.014315400600323255, "bg": 1.435277618005132e-07}, {"x": 0.49310344827586206, "y": 0.5862068965517241, "ox": 0.49310344827586206, "oy": 0.5862068965517241, "term": "video", "cat25k": 48, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 12, "ncat": 8, "s": 0.6620689655172414, "os": 0.035557607942738406, "bg": 1.094621843208436e-07}, {"x": 0.496551724137931, "y": 0.0034482758620689655, "ox": 0.496551724137931, "oy": 0.0034482758620689655, "term": "complete", "cat25k": 8, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 2, "ncat": 8, "s": 0.09310344827586206, "os": -0.10528746247979681, "bg": 1.3393585538656394e-07}, {"x": 0.1482758620689655, "y": 0.2482758620689655, "ox": 0.1482758620689655, "oy": 0.2482758620689655, "term": "normal", "cat25k": 24, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 4, "s": 0.5724137931034482, "os": 0.01662433618102055, "bg": 3.54259833681739e-07}, {"x": 0.5, "y": 0.12413793103448276, "ox": 0.5, "oy": 0.12413793103448276, "term": "say", "cat25k": 16, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 8, "s": 0.15517241379310345, "os": -0.07711844839528977, "bg": 1.530043903844799e-07}, {"x": 0.32413793103448274, "y": 0.1896551724137931, "ox": 0.32413793103448274, "oy": 0.1896551724137931, "term": "before", "cat25k": 20, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 6, "s": 0.33448275862068966, "os": -0.030247056107134615, "bg": 7.926242851542246e-08}, {"x": 0.15172413793103448, "y": 0.19310344827586207, "ox": 0.15172413793103448, "oy": 0.19310344827586207, "term": "actually", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 2.591507982514059e-07}, {"x": 0.4241379310344828, "y": 0.41379310344827586, "ox": 0.4241379310344828, "oy": 0.41379310344827586, "term": "still", "cat25k": 32, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 7, "s": 0.44482758620689655, "os": -0.004386977603324876, "bg": 1.5752458143526494e-07}, {"x": 0.3275862068965517, "y": 0.041379310344827586, "ox": 0.3275862068965517, "oy": 0.041379310344827586, "term": "anything", "cat25k": 12, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 6, "s": 0.21379310344827587, "os": -0.058416070191641654, "bg": 2.3684759015471936e-07}, {"x": 0.6482758620689655, "y": 0.5103448275862069, "ox": 0.6482758620689655, "oy": 0.5103448275862069, "term": "from", "cat25k": 40, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 10, "ncat": 12, "s": 0.23448275862068965, "os": -0.05818517663357192, "bg": 1.9335488962917726e-08}, {"x": 0.42758620689655175, "y": 0.12758620689655173, "ox": 0.42758620689655175, "oy": 0.12758620689655173, "term": "long", "cat25k": 16, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 7, "s": 0.19655172413793104, "os": -0.060725005772338955, "bg": 8.711747764933794e-08}, {"x": 0.15517241379310345, "y": 0.6310344827586207, "ox": 0.15517241379310345, "oy": 0.6310344827586207, "term": "by", "cat25k": 56, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 14, "ncat": 4, "s": 0.893103448275862, "os": 0.12930039251904873, "bg": 1.0746070242558572e-08}, {"x": 0.15862068965517243, "y": 0.19655172413793104, "ox": 0.15862068965517243, "oy": 0.19655172413793104, "term": "far", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 1.933928867388757e-07}, {"x": 0.5586206896551724, "y": 0.41724137931034483, "ox": 0.5586206896551724, "oy": 0.41724137931034483, "term": "'ve", "cat25k": 32, "ncat25k": 48, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 10, "s": 0.2413793103448276, "os": -0.053567305472177335, "bg": 0.0}, {"x": 0.3310344827586207, "y": 0.4206896551724138, "ox": 0.3310344827586207, "oy": 0.4206896551724138, "term": "during", "cat25k": 32, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 6, "s": 0.5344827586206896, "os": 0.012006465019625948, "bg": 1.3567372183264537e-07}, {"x": 0.33448275862068966, "y": 0.2517241379310345, "ox": 0.33448275862068966, "oy": 0.2517241379310345, "term": "i 've", "cat25k": 24, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 6, "s": 0.4103448275862069, "os": -0.0161625490648811, "bg": 0.0}, {"x": 0.2517241379310345, "y": 0.3448275862068966, "ox": 0.2517241379310345, "oy": 0.3448275862068966, "term": "sure", "cat25k": 28, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 5, "s": 0.5586206896551724, "os": 0.014315400600323255, "bg": 2.171126037421691e-07}, {"x": 0.6517241379310345, "y": 0.3482758620689655, "ox": 0.6517241379310345, "oy": 0.3482758620689655, "term": "an", "cat25k": 28, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 7, "ncat": 12, "s": 0.1103448275862069, "os": -0.10043869776033247, "bg": 2.50283269946285e-08}, {"x": 0.43103448275862066, "y": 0.6344827586206897, "ox": 0.43103448275862066, "oy": 0.6344827586206897, "term": "meeting", "cat25k": 56, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 14, "ncat": 7, "s": 0.803448275862069, "os": 0.08012006465019625, "bg": 3.476035861169511e-07}, {"x": 0.6551724137931034, "y": 0.6379310344827587, "ox": 0.6551724137931034, "oy": 0.6379310344827587, "term": "students", "cat25k": 56, "ncat25k": 58, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 14, "ncat": 12, "s": 0.4586206896551724, "os": -0.0018471484645578296, "bg": 2.5388865506991505e-07}, {"x": 0.6137931034482759, "y": 0.6896551724137931, "ox": 0.6137931034482759, "oy": 0.6896551724137931, "term": "panopto", "cat25k": 64, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 11, "s": 0.696551724137931, "os": 0.04271530824290001, "bg": 0.0041564039408867}, {"x": 0.43448275862068964, "y": 0.006896551724137931, "ox": 0.43448275862068964, "oy": 0.006896551724137931, "term": "\u2019m", "cat25k": 8, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 2, "ncat": 7, "s": 0.1413793103448276, "os": -0.088894019856846, "bg": 0.0}, {"x": 0.5620689655172414, "y": 0.2, "ox": 0.5620689655172414, "oy": 0.2, "term": "no", "cat25k": 20, "ncat25k": 48, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 10, "s": 0.11379310344827585, "os": -0.0958208265989379, "bg": 3.201279487385519e-08}, {"x": 0.4379310344827586, "y": 0.010344827586206896, "ox": 0.4379310344827586, "oy": 0.010344827586206896, "term": "i \u2019m", "cat25k": 8, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 2, "ncat": 7, "s": 0.1413793103448276, "os": -0.088894019856846, "bg": 0.0}, {"x": 0.33793103448275863, "y": 0.04482758620689655, "ox": 0.33793103448275863, "oy": 0.04482758620689655, "term": "little", "cat25k": 12, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 6, "s": 0.21379310344827587, "os": -0.058416070191641654, "bg": 9.617671226994122e-08}, {"x": 0.3413793103448276, "y": 0.04827586206896552, "ox": 0.3413793103448276, "oy": 0.04827586206896552, "term": "a little", "cat25k": 12, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 6, "s": 0.21379310344827587, "os": -0.058416070191641654, "bg": 0.0}, {"x": 0.5655172413793104, "y": 0.4862068965517241, "ox": 0.5655172413793104, "oy": 0.4862068965517241, "term": "lot", "cat25k": 36, "ncat25k": 48, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 10, "s": 0.2931034482758621, "os": -0.039482798429923804, "bg": 3.5708180420881427e-07}, {"x": 0.5689655172413793, "y": 0.4896551724137931, "ox": 0.5689655172413793, "oy": 0.4896551724137931, "term": "a lot", "cat25k": 36, "ncat25k": 48, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 9, "ncat": 10, "s": 0.2931034482758621, "os": -0.039482798429923804, "bg": 0.0}, {"x": 0.16206896551724137, "y": 0.25517241379310346, "ox": 0.16206896551724137, "oy": 0.25517241379310346, "term": "things", "cat25k": 24, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 4, "s": 0.5724137931034482, "os": 0.01662433618102055, "bg": 1.3515077975107225e-07}, {"x": 0.16551724137931034, "y": 0.20344827586206896, "ox": 0.16551724137931034, "oy": 0.20344827586206896, "term": "prerecorded", "cat25k": 20, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 5, "ncat": 4, "s": 0.4793103448275862, "os": 0.002539829138767033, "bg": 9.168610751724207e-05}, {"x": 0.6172413793103448, "y": 0.5689655172413793, "ox": 0.6172413793103448, "oy": 0.5689655172413793, "term": "out", "cat25k": 44, "ncat25k": 53, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 11, "s": 0.3758620689655172, "os": -0.027707226968367582, "bg": 5.932998867623792e-08}, {"x": 0.7758620689655172, "y": 0.5724137931034483, "ox": 0.7758620689655172, "oy": 0.5724137931034483, "term": "when", "cat25k": 44, "ncat25k": 92, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 19, "s": 0.04827586206896551, "os": -0.15885476795197412, "bg": 9.221772001821981e-08}, {"x": 0.3448275862068966, "y": 0.05172413793103448, "ox": 0.3448275862068966, "oy": 0.05172413793103448, "term": "us", "cat25k": 12, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 6, "s": 0.21379310344827587, "os": -0.058416070191641654, "bg": 1.4644557121402588e-08}, {"x": 0.6724137931034483, "y": 0.6931034482758621, "ox": 0.6724137931034483, "oy": 0.6931034482758621, "term": "one", "cat25k": 64, "ncat25k": 63, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 16, "ncat": 13, "s": 0.5206896551724138, "os": 0.009928422996998365, "bg": 5.83765506428529e-08}, {"x": 0.16896551724137931, "y": 0.25862068965517243, "ox": 0.16896551724137931, "oy": 0.25862068965517243, "term": "synchronous meetings", "cat25k": 24, "ncat25k": 19, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 4, "s": 0.5724137931034482, "os": 0.01662433618102055, "bg": 0.0}, {"x": 0.7620689655172413, "y": 0.4241379310344828, "ox": 0.7620689655172413, "oy": 0.4241379310344828, "term": "hard to", "cat25k": 32, "ncat25k": 82, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 8, "ncat": 17, "s": 0.041379310344827586, "os": -0.16832140383283306, "bg": 0.0}, {"x": 0.5482758620689655, "y": 0.1310344827586207, "ox": 0.5482758620689655, "oy": 0.1310344827586207, "term": "due", "cat25k": 16, "ncat25k": 43, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 9, "s": 0.11724137931034483, "os": -0.09351189101824058, "bg": 2.478048115459658e-07}, {"x": 0.8172413793103448, "y": 0.5758620689655173, "ox": 0.8172413793103448, "oy": 0.5758620689655173, "term": "none", "cat25k": 44, "ncat25k": 111, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 11, "ncat": 23, "s": 0.027586206896551724, "os": -0.20803509582082658, "bg": 7.949850472665374e-07}, {"x": 0.4413793103448276, "y": 0.013793103448275862, "ox": 0.4413793103448276, "oy": 0.013793103448275862, "term": "participate", "cat25k": 8, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 2, "ncat": 7, "s": 0.1413793103448276, "os": -0.088894019856846, "bg": 7.363913045932898e-07}, {"x": 0.5724137931034483, "y": 0.05517241379310345, "ox": 0.5724137931034483, "oy": 0.05517241379310345, "term": "did", "cat25k": 12, "ncat25k": 48, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 10, "s": 0.07241379310344827, "os": -0.12398984068344493, "bg": 9.441413615508329e-08}, {"x": 0.6758620689655173, "y": 0.2620689655172414, "ox": 0.6758620689655173, "oy": 0.2620689655172414, "term": "sometimes", "cat25k": 24, "ncat25k": 63, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 6, "ncat": 13, "s": 0.0689655172413793, "os": -0.13091664742553683, "bg": 8.014179699040978e-07}, {"x": 0.7517241379310344, "y": 0.017241379310344827, "ox": 0.7517241379310344, "oy": 0.017241379310344827, "term": "without", "cat25k": 8, "ncat25k": 77, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 2, "ncat": 16, "s": 0.02068965517241379, "os": -0.23643500346340335, "bg": 1.6423126301943338e-07}, {"x": 0.25517241379310346, "y": 0.13448275862068965, "ox": 0.25517241379310346, "oy": 0.13448275862068965, "term": "via", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 1.8522310256476167e-07}, {"x": 0.503448275862069, "y": 0.05862068965517241, "ox": 0.503448275862069, "oy": 0.05862068965517241, "term": "lab", "cat25k": 12, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 8, "s": 0.13448275862068967, "os": -0.09120295543754328, "bg": 6.190392499585384e-07}, {"x": 0.506896551724138, "y": 0.13793103448275862, "ox": 0.506896551724138, "oy": 0.13793103448275862, "term": "could", "cat25k": 16, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 8, "s": 0.15517241379310345, "os": -0.07711844839528977, "bg": 7.938492349582306e-08}, {"x": 0.3482758620689655, "y": 0.1413793103448276, "ox": 0.3482758620689655, "oy": 0.1413793103448276, "term": "work well", "cat25k": 16, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 6, "s": 0.2724137931034483, "os": -0.04433156314938813, "bg": 0.0}, {"x": 0.25862068965517243, "y": 0.5896551724137931, "ox": 0.25862068965517243, "oy": 0.5896551724137931, "term": "sessions", "cat25k": 48, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 12, "ncat": 5, "s": 0.8206896551724138, "os": 0.08473793581159086, "bg": 1.5800088359670612e-06}, {"x": 0.44482758620689655, "y": 0.14482758620689656, "ox": 0.44482758620689655, "oy": 0.14482758620689656, "term": "recordings", "cat25k": 16, "ncat25k": 34, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 7, "s": 0.19655172413793104, "os": -0.060725005772338955, "bg": 1.8538687924362152e-06}, {"x": 0.35172413793103446, "y": 0.06206896551724138, "ox": 0.35172413793103446, "oy": 0.06206896551724138, "term": "issues", "cat25k": 12, "ncat25k": 29, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 3, "ncat": 6, "s": 0.21379310344827587, "os": -0.058416070191641654, "bg": 1.1990467738021176e-07}, {"x": 0.2620689655172414, "y": 0.1482758620689655, "ox": 0.2620689655172414, "oy": 0.1482758620689655, "term": "something", "cat25k": 16, "ncat25k": 24, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 4, "ncat": 5, "s": 0.3413793103448276, "os": -0.027938120526437307, "bg": 1.3651961623061694e-07}, {"x": 0.5103448275862069, "y": 0.020689655172413793, "ox": 0.5103448275862069, "oy": 0.020689655172413793, "term": "hour", "cat25k": 8, "ncat25k": 39, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 2, "ncat": 8, "s": 0.09310344827586206, "os": -0.10528746247979681, "bg": 2.786340434126886e-07}, {"x": 0.5758620689655173, "y": 0.0, "ox": 0.5758620689655173, "oy": 0.0, "term": "harder", "cat25k": 4, "ncat25k": 48, "neut25k": 0, "neut": 0, "extra25k": 0, "extra": 0, "cat": 1, "ncat": 10, "s": 0.05172413793103448, "os": -0.152158854767952, "bg": 2.457906946994678e-06}], "docs": {"categories": ["best", "worst"], "labels": [0, 1], "texts": ["Q12: Which online instructional methods have worked best for you?\t\n1:1 conversations with my professors have worked the best since all my classes are discussion-based and can be quite chaotic with bigger groups.\n2. Moodle writing discussions and recorded lectures\nA combination of all of them works best because it keeps the class moving and more engaging. I do really like the small group discussion though.\nA combination of Zoom and Moodle assignments has proven to be effective.\naccess to textbook online  attending lectures  contacting TAs/professor for help\nActivities and online worksheets to test knowledge of concepts\nall\nall\nAll good\nAll have been about the same level of success for me.\nAll have been fine\nAll have been fine\nAll have been fine and good\nAll have worked pretty well. However, it just does not feel the same having to learn through a screen.\nAll have worked very well. I have appreciated the free access to online textbooks on red shelf\nAll of the above have been great!\nall of them\nAll of them have worked equally.\nAll of them have worked pretty well!\nall of them have worked well\nAll of them have worked.\nAll of them worked.\nAll of them, especially pre-recored and recorded options. I appreciated professors' presence and attention to my needs. Inviting speakers over Zoom was fun and helpful too!\nAll of these methods have been helpful.\nAll the ones that I have been doing for my classes are okay\nAll work, but the live office hours and discussions are most effective\nAll. Geology online doesn't work as well since it was already reverse classroom and now we can't do in-class activities.\nalll of my courses have been on zoom\nAny of them. Especially those that allow me and others to take our time in doing work - many, myself included, are under serious financial or family stress at this time, and so being able to set our own deadlines (to a point) has been helpful.\nAs there has not been much variety of format, I do not have much of a comparison to make.\nassigned readings and recorded lectures\nAssignments posted on Moodle to be done at my own pace\nAsymmetrical lectures, as my schedule at home is very different than what is was at school\nAsynchronous because I have more flexibility in what I would like to do\nAsynchronous because you always have the option of rewatching the lessons if needed.\nasynchronous classes are both easier in content and more convenient for me, as I have to get up very early to attend morning classes.\nAsynchronous has worked best for me.\nAsynchronous is nice. Can take classes on own schedule, and the flexibility is much appreciated right now\nAsynchronous learning\nAsynchronous learning\nAsynchronous learning has been nice because it gives flexibility, but it does feel impersonal. Zoom classes have been good to get some social contact, but are very hard in bigger classes.\nAsynchronous learning worked best for me because my internet connection is not very reliable, so it gives me more flexibility and time.\nAsynchronous lectures\nAsynchronous lectures.\nAsynchronous materials released has worked best for me.\nasynchronous meetings have been the nicest, though it is nice to see my classmates face to face. but the time comitment is hard given the current pressures.\nAsynchronous methods have worked best for me.\nasynchronous recorded videos and discussion forums\nAsynchronous Zoom lectures\nasynchronous.\nAsynchronous.\navailability to watch lectures whenever\nboth\nBoth are fine.\nBoth had their advantages and disadvantages.\nboth have worked fine\nBoth have worked fine, but I prefer recorded lectures because I can find the time that works best for me to go through the material.\nBOth have worked really well\nBoth have worked well I like the combination of them\nBoth have worked well, but I like synchronous learning better.\nBoth have Zoom and Microsoft Teams have worked equally well. My Econ professor has been recording the lectures which are nice to refer back to for review. And my Sociology professor has been recording 15-minute recaps of the readings which has been really helpful.\nBoth in different ways--  Zoom has been good with certain classes that I need to ask questions in (real-time)  Whereas, pre-recorded classes are good with other classes where they just lecture and then there are other opportunities to ask questions if need be.\nBoth of them work good for me.\nboth work fine for me since I'm in the same time zone\nBoth work very well!\nBoth work, Zoom is nice because discussion is slightly more engaging and you don't feel like you're speaking into the void. It's also nice to see people.\nBoth work, Zoom probably works better than the discussion boards for me\nBoth work.\nboth worked well\nBoth Zoom and Moodle have been fine, but I have more trouble with keeping up with the pre-recorded lectures.\nBoth Zoom and Moodle have proven pretty reliable for classes\nBoth! Zoom is great for my smaller classes and for small group meetings and office hours with professors, but Panapto works pretty smoothly for my bigger lecture based classes.\nBoth.\nClass recording.\nCombination with focus on synchronous learning\nDefinitely not slack. While I don\u2019t like zoom, it\u2019s the best solution for class. It keeps people engaged in the schedule of having class, of keeping it at the forefront of our thinking. Also discussion can happen\nDefinitely the discussion boards, because I don\u2019t need consistent great WiFi or a quiet space, both of which have been difficult to find\nDefinitely the zoom meetings, since they provide much needed structure in these uncertain times.\nDiscussion boards\nDiscussion on zoom in breakout rooms\nEach instructional method felt most appropriate for the class to which it was applied, and all have worked relatively well.\nEach of the class formats has worked well for its course (synchronous for a language course and asynchronous for lecture courses)\nEach works well for the specific class, but overall I prefer watching pre-recorded lectures because of the ability to pause and rewatch certain portions, formulate questions, and email the professor, because I find that I can never think of questions fast enough or really even keep up with the live Zoom lectures.  I think that Haverford academics are overall really unnecessarily difficult in a way that doesn't benefit anyone's learning, so I think the easing of the workload across the board was a positive change that has allowed me to engage more deeply with the material despite not having access to class or campus resources. I can only imagine how much it would have helped me and my learning if Haverford academics were always this small amount less demanding.\nEDU200 CLC at Bryn Mawr.\nEveryone has used zoom besides a class that is solely using moodle as a discussion forum. I think everything has been working well.\nEverything has been accessible and worked reasonably well for me.\nEverything through Zoom has worked surprisingly well, despite timezones\nface to face contact through zoom\nFor discussion based classes, live discussion sections and moodle posts have worked well.\nFor lectures and discussions, I have found Zoom works well.\nGenerally, breakout rooms have been most effective for me, as I tend to gravitate towards smaller group discussions, and in some ways, this has been superior to the in-person experience, as it allows for greater variation in discussions among peers with whom I might not otherwise have contact\nGoing to actual zoom meetings has helped me be more engaged with the class and probably learn more, but as I am in another country and timezone, being able to watch lectures asynchronously has been tremendously helpful.\nGood\nHaving a live lecture made a big difference for me, and I most liked the system with retained writing assignments that were adjusted (with extensions given more freely) and with retained reading assignments.\nHaving a mix of asynchronous and synchronous have worked. Having a few zoom meetings a week ans also lecture videos and slack/piazza for questions or responses to a video/reading have worked for me\nHaving consistent Zoom classes\nHaving supplementary lectures, readings, and videos to complete on our own time is so much easier than staying structured around the normal class schedule.\nhaving the classes be recorded so I can watch them again.\nHonestly I am not the best person to ask since I don't have any zoom classes. But I can say that the online assignments have worked for me since they are essentially the same or very similar to the ones we had before\nHonestly, I dislike them all: 1) I never learn well through passive reading/listening (as a result, my course choices are largely interactive/participatory), but... 2) I do not use a cell phone, because I get nervous and cannot think on a phone; same applies to video streaming myself - I am actually adapting now as I am forced to zoom, but still, in every zoom class, at least 70% of my attention is on the fact that I am on zoom, which is extremely stupid and frustrating but I cannot stop this distraction. 3) Posting in a discussion forum simply doesn't teach me anything. I seldom read others posts, which is my own fault, but I have so much reading piling up already, so responding to others is simply not a priority. 4)  Essay writing is always a painful process, but I do learn from it. Because I am in front of a screen all day all day long, this process is getting even more unbearable. Still, I feel this is by far the most fruitful effort.\nHonestly, I've found it to be incredibly difficult to focus during the synchronous zoom class meetings and find my engagement in them slipping away more and more as time goes on, with the fault not falling on the professor but just the medium itself. For me personally, I'm not sure if there's really an online instructional method that I can really praise because it really just doesn't work for me.\nHonestly, they have been sub-optimal as there is a general lack of motivation to work.\nI definitely prefer synchronous over asynchronous classes, and the breakout room discussions are also helpful.\nI don't feel that these methods work for me.\nI don't like any of them, but if I had to choose, it would have to be Zoom.\nI enjoy a mix of them both. I think it is nice to have flexibility, but the structure is also beneficial to keep me focused and motivated. I actually think some of the asynchronous lectures have been more beneficial to my learning because I am able to pause videos, write down questions as I go, and rewatch them as needed. My discussion-based lectures (like my writing seminar and Spanish) definitely benefit from being synchronous, but my science courses do well using a mix of synchronous and asynchronous teaching.\nI enjoy meeting with actual people synchronously because it allows me to be social and have a somewhat organic conversation. Pre-recorded lectures are fine.\nI enjoy that my Stats professor records and posts his zoom lectures online after class, as that makes the information easily accessible for students if they are unable to make the class. Overall I have enjoyed all the combinations of instructional methods my professors have used.\nI enjoy the synchronous classes\nI enjoy the zoom meetings because I get to see the faces of my classmates. I also value discussing the books and articles in my classes.\nI feel like office hours have been most useful.\nI find that the synchronous classes are most helpful, especially in STEM, where asking questions during the lectures can be very helpful.\nI find that zoom lectures and moodle discussion boards work pretty well.\nI find the panopto lectures and zoom class discussion model to be most engaging and educational. Group work is crucial right now as it lets me continue to stay connected with my classmates.\nI found that live Zoom lecture emulated regular lecture the best.\nI found Zoom to work quite well for me\nI guess asynchronous. But I hate most of it. I\u2019m appreciative of the kindness of the faculty, but zoom is truly a miserable existence and no amount of kindness and \u201ccheck ins\u201d from teachers will fix that.\nI guess Zoom? It's really the only thing all of my professors use. I do think it's a pretty good video conference program though.\nI have liked zoom just fine, I like the breakout room feature and think it helps give the meeting some texture and variety. I am not super enthusiastic about the technology but it is the closest we can get to what in person class would be like.\nI have not experienced a large variety of instructional methods, partly because all of my classes are upper-level Humanities courses.\nI have the same format for all classes. This works well for my accounting class because there are over a hundred students in that class.\nI haven\u2019t had any other instructional methods used to compare with\nI honestly can't really tell if I'm learning anything.\nI like getting to see people and have conversations over zoom, I have also enjoyed podcasts created by my professor.\nI like most having a narrated power point to look at before class and then have a shortened class in the form of a zoom discussion\nI like shorter lectures-- I feel as though more frequent shorter lectures are working best for me\nI like synchronized classes because it's the closest thing to being in actual class. It's nice to have structure to my schedule and to see everyone in an unscripted environment.\nI like the articles and discussion boards for seminar style classes.\nI like the classes that have basically continued how they were going before best. Those that still meet regularly and expect a similar level of discussion and preparation.\nI like the combo of synchronous and asynchronous learning because it takes a little of the pressure off the student during this time.\nI like the discussion boards a lot. Allowing people to create thoughtful comments on their own time is a nice less stressful way to do things.\nI like the live lectures on Zoom because it gives me the opportunity to see faces and interact with people\nI like the online office hours. It is nice that some professors added additional office hours incase we need extra help\nI like the prerecorded discussions because I can go back and listen again for things I missed or need to know.\nI like the prerecorded lectures.\nI like the pre-recorded panopto/Powerpoint presentations with accompanying audio narration- it is easy to follow, pause as needed, and go back and reference later.\nI like the recorded lectures and I think Zoom can work if teachers go out of there way to incorporate the class.  I am in some classes where the teachers do this well and others where they don't and when they don't it leads to less engagement and less learning.\nI like the synchronous classes especially in the stem field because it allows us to be more interactive.\nI like Zoom because I feel like having a synchronous meet-up helps keep me motivated. I also like Panopto, though, because being able to pause and rewind lectures is very helpful for taking notes\nI like Zoom lectures and breakout rooms for smaller discussions\nI liked the recorded lectures\ni love the asynchronous style.\nI only have one zoom class and I like that one the most, it makes me feel like there is still some structure to my schedule.\nI prefer asynchronous learning because I like to work at my own pace and not stress too much about deadlines or my own availability\nI prefer synchronous meetings, as I feel they preserve the learning format my classes were designed for the best.\nI prefer the discussions. Lectures are very hard to follow and my computer glitches and I miss things. Lectures are also just draining and not interesting online. I feel myself losing focus often.\nI prefer the readings outside of class and discussion in class over leacture styles. It is very hard for me to focus on lectures.\nI prefer the Zoom classes\nI really dislike both for different reasons. Zoom is slightly preferable due to more possible interaction.\nI really like online, pre-recorded lectures.\nI really liked the Google applications and Zoom has worked well.\nI suppose Zoom has worked best? The other two methods put an unnecessary and unhelpful burden on students.\nI think having the combination is effective.\nI think I feel more comfortable with asynchronous learning rather than scheduled zoom classes.\nI think in general, none of the methods that have changed are super good for me. I think one-on-one meetings with faculty have probably been the most effective, as they are the closest to the normal experience of meeting with people.\nI think it depends on the course; both are alright but since I have a time difference I prefer recorded lectures\nI think live Zoom courses are better for learning, but since I'm on the West Coast, I'm not a fan of waking up early in the morning to attend them.\nI think my synchronous classes have worked the best.\nI think prerecorded classes have worked best for me\nI think readings for my humanities classes paired with the podcasts my teacher has been releasing works well.\nI think that synchronous discussion works well. For my smaller classes, people generally participate about as much now as they did when the class was in-person. I really like the breakout room/small group discussion option on zoom. It mimics in-person learning pretty well.\nI think that the videos and quizzes to check understanding are very effective.\nI think that zoom with the option to watch a recorded video afterwards for people in different time zones is the best instructional method.\nI think the recorded lectures have kind of worked, at least better than zoom.\nI think the videos made by professors are the best methods, because I can pause these videos, resume later if I have technical difficulties, and write down my questions as I go.\nI think this question is slightly flawed since some classes work better with an online format than others. My language class seemed to adapt the best to the online format due to the lack of changes in meeting time and the similarity with in-class activities. In addition, it is able to benefit from the use of Google Doc activities (which were already present for class activities) and break out rooms for discussions.\nI think Zoom\nI think Zoom has been great for lectures and discussions.\nI think Zoom is the best option available for connecting with others virtually. However, it is hard to stay focused and the wifi in my house isn't very good, so I often experience lags.\nI think zoom lectures work best for me, it is sometimes hard to get the work done without the structure of going to class.\nI think Zoom works okay for meeting over video, although certainly not perfect. I like the lecture videos my professor records using Panopto.\nI wish I had asynchronous because I don't like waking up at 7am for a class.\nI\u2019d say Zoom can be nice sometimes.\nI\u2019ve only used zoom\nIdk\nI'm fine with all of them.\nI'm not a big lecture person in general. For one of my classes, some instruction has been replaced by podcasts and news videos, which I have gotten a lot out of. Another of my professors has always posted detailed lecture notes on Moodle, and I'm using those instead of ever watching lecture videos.\nI'm unsure\u2014I recently just became well again, and I haven't been able to do that much coursework. All I know is that asynchronous courses are often, as a result of their nature, largely self-paced. This is nice at times, but also stressful\u2014what if I leave too much for the last minute? But that is extreme. Overall, I'd say the way we're working in one of my classes, Classical Mythology with Professor Silverblank, is effective: we watch pre-recorded lectures, participate in optional discussions via Slack, and have all semester to complete relevant course assignments.\nIn person class\nIn person Zoom lectures/discussions/TA office hours are the best, and of course moodle. Also my physics labs were made virtual by our profs recording themselves doing the lab, which was probably the closest we could get.\nIt depends on the course, but I think Zoom lectures work well\nIt has really helped me to have synchronous class meetings and stay motivated and engaged.\nIt\u2019s been fine\nIt's worked fine, not as well as real lecture but about as good as can be expected I suppose\nI've enjoyed Panopto as I can pause and make sure I've written everything down. I also get to watch it on my own time and with breaks in between if needed.\nI've liked the discussion where you can see everyone.\nI've only had synchronous virtual zoom meeting and occasionally watch the recording outside class time, and both worked equally well for me.\nI've only used zoom, another professor though has posted video lectures which have been helpful as well.\nLectures\nLectures and break out rooms on zoom\nLectures through Zoom or pre-recorded video lectures from my professors are BY FAR the best for learning. They are the closest to the classroom setting, and make me feel some semblance of a Haverford setting.\nLectures. (Class discussion is so difficult)\nLive classes have been the best for me.\nLive classes through zoom\nLive lectures\nLive lectures and screensharing examples\nLive Lectures with lots of interaction with students.\nlive lectures, group discussions, and posted videos of lectures\nLive lessons for sure\nLive Zoom\nLive Zoom lectures have been most helpful, though pre-recorded lectures make more sense for all students since it is not always possible for students to attend them given their time zone. One of my professors records the live lecture so we can have either one, which I think is extremely helpful.\nlive zoom lectures.\nLive Zoom meetings.\nLive Zoom sessions for smaller seminars.  Posting of lecture/office hours recordings.\nLIVE zoom!\nLow-key... Twitter Zoom is cool too\nMath labs conducted via Zoom breakout rooms Online Peer Tutoring, Math Question Center, Calculus Resource Center, Office Hours\nMicrosoft Teams and Whatsapp\nMoodle\nMoodle\nMoodle Discussion Forums\nMoodle forum and Voicethread\nMoodle lecture posts\nMoodle quizzes/activities and power point slides for my large Oceanography lecture --&gt; learning on my own time, but still having to be accountable Readings + reactions + forums\nMy favorite method has been classes which divide their time between synchronous and asynchronous measures.\nMy internet connection is not strong, so Zoom is difficult for me. I like the discussion board posts.\nMy zoom meeting works well because it is only 4 students that meet once a week with our professor. The other methods have been okay, I just feel very disconnection from professors and fellow students.\nN/a I haven\u2019t been a big fan\nNeither have worked that well to be honest.\nneither really work, but i guess synchronous\nNeither. I don\u2019t watch the recorded lectures and I don\u2019t attend the zoom lectures. I strongly dislike online learning and find nearly impossible to keep up with. Additionally, one of my professors is legitimately flooding my inbox with emails. I can\u2019t keep up.\nNeither. I find it extremely difficult to retain information to the same degree as I did on campus.\nNon synchronous lectures via PowerPoint\nNone\nnone -- due to a number of health issues, my participation has been extremely sporadic and it has been very difficult to engage.\nNone are great but the zoom lectures are all we have.\nNone are the same as being in-person, but they are all running smoothly. Largely the result of professor flexibility and a willingness to adjust expectations and demands of students.\nNone have been goos\nNone of them work that well for me\nNone of these quite work best for me. I tend to zone out a lot and there are often a lot of technical issues. I'd say the Ipad sketches were most effective but a lot is left to be desired.\nnone to be honest\nNone. I have issues with social anxiety and attention that I\u2019ve learned are exacerbated by online learning.\nNone. They all utterly fail to engage my attention.\nNothing can recreate a seminar outside of the classroom, since on Zoom calls everyone invariably talks over each other, but Zoom is the best alternative.\nOffice hours\nOnline classes\nOnline lecture with frequent activities and breakout rooms for class discussion\nOnline lectures\nOnline lectures are achieving what they could achieve\nonline live lectures\nOnline videos because I can always go back and rewatch the videos.\nOnly one method, but it's okay.\nOptional weekly class meeting since I take care of a two year old during the day and therefore cannot attend these meetings.\nPanapto\npanapto and chat form\nPanopto and zoom have been the best in my opinion.\nPanopto is especially helpful.\nPanopto lectures\nPanopto recorded lectures with less frequent zoom checkins\nPanopto works well for lectures, though it can be hard to focus. Zoom is a good platform but classes end up being shorter and lower quality because it's fatiguing to do them like a normal class.\nPanopto. I find Zoom classes focused on discussion to be unproductive and forced.\nPosted slides\nPre recorded lectures\npre-prepared lectures\nPre-recorded lecture courses.\nPrerecorded lecture works the best.\npre-recorded lectures and live zoom classes\nPre-recorded lectures with an additional synchronous meeting through Zoom for discussion or clarification has worked best for me\nPre-recorded lectures, Zoom\nPre-recorded lectures/videos.\nPre-recorded posted lectures. Posting to class forums. SMALL group zoom sessions.\nProgramming projects\nReadings and then commenting and responding to others on a forum, with a short, once weekly zoom meeting.\nReal-time!\nRecorded classes\nRecorded lecture\nRecorded lecture\nRecorded lectures\nrecorded lectures\nRecorded lectures are great because I can watch them on my own time, rewind when I need to go over something again, and pause when I need to write something important down before it is erased.\nrecorded lectures because I am in a different time zone & my classes would be VERY early\nRecorded lectures have worked best\nRecorded lectures send PDFs\nRecorded Lectures will likely prove most useful\nrecorded videos\nrecorded zoom live lectures, since I am in a different time zone\nRecording\nRecordings and small assignments\nrecored lectures are really nice to have.\nregular zoom meeting\nRegular zoom meetings\nRegular zoom meetings twice a week.\nScheduled discussions and recorded lessons\nSeminar with synchronous meetings (only bc I am in the same time zone and have good internet).\nShort Zoom classes have worked. Long Zoom classes have been hard and not helpful (anything over 2 hours is no longer useful, and 1.5 hours at max is ideal)\nSince most of my classes have either severely reduced the workload or else kept things as they would have otherwise been, not much has changed, but of what has, the online 'normal' zoom classes are working best for me.\nSmall group discussion and group collaboration on google docs have worked best for me.\nSmall Zoom breakout sessions and check-ins.\nSmaller group Zoom meetings with professors, Synchronous Zoom lectures/seminars, asynchronous lab work\nSome of the online lectures - depending on the professor.\nStructured readings and postings with access to office hours have worked best for me.\nStudent presentations- researching our own topics and then presenting them to the other students in the class\nSynchronized Zoom classes.\nSynchronous class sessions\nSynchronous classes by far.\nSynchronous classes have been effective for lecture-style classes, but less so for discussion-based classes or more interactive lecture classes.\nSynchronous classes probably but all are bad. I\u2019m not learning well\nSynchronous discussion sessions have been best for me, although they have also resulted in more work outside of class to prepare for discussion sessions in my class that used to be a lecture and now has both synchronous and asynchronous parts\nSynchronous lab sections and office hours, and prerecorded lectures\nSynchronous learning is okay, but the workload has been excessive and the deadlines are also unreasonable.\nSynchronous learning only when the class was small.\nSynchronous learning through Zoom classes is the best option in these circumstances. Though staring at the computer screen is more fatiguing than being in class, it is the best way to continue interacting with professors and students. Breakout rooms are especially useful for simulating in-class discussion.\nSynchronous meetings have been the most effective method, as it provides structure to my week/schedule and subconsciously increases the \"seriousness\" of class, which I believe is very important.\nSynchronous Zoom lecture\nsynchronous zoom lectures seem to be best for me\nSynchronous Zoom meetings.\nSyncrhonous class is a blessing, I know it's not possible for everyone, but it is DEFINITELY better. Participation in online moodle discussion groups, or weekly journal entries, it's superfluous. It feels like I write a book report every week; also, it really impairs my time management - sometimes I have to wait for my classmates to respond, and they're on their own schedules!\nTeaching on white boards at home via zoom\nThe ability to record the lectures. The ability to access the lectures in almost no time.\nThe asynchronous have been much better.\nthe asynchronous lectures\nThe asynchronous option\nThe board teaching has worked best for me.\nThe class with only some zoom meetings and revised syllabus. Oceanography a little less difficult in terms of time spent in actual zoom classes but that\u2019s a whole other bag\nThe classes I have been having are fine, it is easy enough to ask questions during lecture\nThe classes that stayed the same - math and death. the workload is about the same, which I appreciate - the workload for physics has really increased since we are now responsible for learning the content by ourselves.\nThe discussion classes have been best.\nthe discussion classes on the normal schedule have worked best for me!\nThe discussions over Twitter feel the most similar to class discussions since comments are casual and concise. The Moodle discussions tend to be long and more formal, heading more towards the direction of a brief paper and are very time consuming. They definitely hold a lot more performative pressure.\nThe latter, especially because the discussion is open so we can bring in whatever we're thinking about into the learning.\nThe live classes work substantially better than recorded ones\nthe method for each class has been ideal under these circumstances.\nThe methods that have worked best are going to office hours.\nThe methods that I learn best from are by far the synchronous meetings that include a visual component.\nThe mixture of all have worked well - lecture and some other ways have been fine asynchronous, though most meaningful is class discussion over zoom.\nThe mixture of both has been helpful. It is nice to still have a connection to my professors and classmates over Zoom\nThe moodle forums\nThe most flexible methods are the best. Recorded lectures and labs with some in person support are helpful.\nThe only class I feel particularly confident in is the class where we're still having synchronous lectures that are recorded and uploaded. Keeping a structure to the week is basically the only thing that keeps me on top of the content. For my other three classes, I'm being maintained only by random bursts of hyper-focusing, which tends to make me spend WAY too much time on one part of something and literally no time on other equally important things. Basically, structured classes is the only thing that can convince me deadlines are real.\nThe only class which has made a modification that has benefitted me is the one that severely reduced expectations. In this class, the professor shortened each class meeting but offered two different sessions to attend on each day, both covering the same topic, so I had the choice to attend the later session which was not when the class originally met but which is at a reasonable hour for me while on PST. And, with the shortened class, I have more time to actually do the work for this class.\nThe optional learning has been working very well with my classes and participation and learning has actually been nearly the same as if we were in class, because we can choose to opt out when things are difficult, we have chores/errands for family, Wi-Fi isn't working, etc. and then come back without feeling stress or pressure.   The optional zoom meeting once a week has been much more engaging than Moodle posts, which I find make me far less likely to engage. That being said, I'm an affluent student with financial and physical security so I actually think that Moodle posts are good. The collaborative final project instead of a final essay/exam is also really great, it takes pressure off of everyone.\nthe powerpoints work well for that specific lecture class, but when discussion based classes have tried them they haven't been the 3-5 person group discussions have worked really well for discussion classes the mini quizzes have been great for making sure i do the readings\nThe prior recordings in conjunction with real time office hour explanations have been very helpful for bio. The zoom sessions for my other classes has also been helpful.\nThe readings and the videos probably with online quizzes/worksheets after, some zoom meetings are helpful\nThe recorded sessions are less stressful, but the live sessions make it so I can't procrastinate/get behind on lectures. I have two classes that the live sessions are pretty much optional (one they also provide recorded lectures, and the other they provide lecture notes) and that works best for me I think.\nThe recorded videos have been great due to the time change.\nthe stuff where we don't have to meet all at the same time (like videos)\nThe synchronous classes have been really beneficial for me during this time, and using breakout rooms as a place to work with other students is often a positive experience.\nThe Zoom meetings and pre-recorded lectures for classes that do not line up well with my hours here at home.\nthe zoom meetings are only nice to give me something in my schedule, the asynchronous allows me to do the work I feel able to do.\nThe zoom sessions have worked extremely well\nthese have not worked for me. Lecturing at this time could not be more boring and less interesting especially over zoom.\nThey all are working ok\nThey all have worked well\nthey all work fine. nothing different from being on campus except for zoom\nThey all worked great\nThey are all fantastic, even if the zoom discussions can\u2019t replace the real thing\nThey both work best\nThey both work well. I think going to office hours is very helpful for math classes.\nThey have all worked well\nThey work , but its not worth the money im paying haverford. If haverford tries to instill any sort of room/board/food cost on us its gonna upset everyone\nThey\u2019ve all worked fine\nthey're all fine\nThey're both fine. I definitely don't feel like I am getting the quality of education I would expect from Haverford, I barely have any work to do and it all just feels like fake class that isn't worth my tuition.\nthey've been fine, but hardly comparative to class at school\nThis has been as good as it possibly could be given the circumstances. Professors have been incredibly helpful and flexible.\nTwitter discussion boards\nunsure, panopto lectures and recorded zoom classes and synchronous zoom classes feel most similar to regular learning. twitter and moodle blog works but can get a little confusing and there's a limit to how much I can get out of it.\nVideo lectures have been the most effective for me because they maintain, to a slight degree, the normalcy of \"going to class\" for a specific block of time. I appreciate the real time discussion and ability to ask questions. I find myself considerably more engaged and excited by this format than more asynchronous approaches.\nvideo recording\nVideos\nVideos viewable for 48 hours\nVirtual TA\nWe have only used zoom.\nWeekly zoom check in.\nZoom\nZoom (mostly) and recorded lectures\nZoom and Microsoft teams.\nZoom and moodle, although my internet connection has been extremely spotty so classes go in and out sometimes\nZoom and online forum.\nZoom and Panopto\nZoom and Panopto/Moodle forums\nZoom and recorded lectures.\nZoom because I am less likely to procrastinate since we have to attend class at a certain time.\nZoom breakout rooms, readings, reading responses. One tea her had us all make presentations and then watch each others\u2019 and respond. I loved that\nZoom by an unquantifiable amount.\nZoom calls\nZoom calls have been the best at keeping me accountable.\nZoom class meetings and Google Hangout office hours.\nZoom classes\nZoom classes\nZoom classes\nZoom classes\nzoom classes\nZoom classes and assignments submitted to moodle.\nZoom classes and office hours\nZoom classes but only for economics. This is likely because the pedagogical methods used by my professor are not impeded on zoom.\nzoom classes definitely\nZoom classes have been fine.\nZoom classes have probably been the best for me.\nZoom classes.\nzoom discussions\nZoom discussions and break out rooms. I have also found that having more small groups discussions or question time has been crucial as it is a lot harder to understand lectures online with no visual aids.\nzoom discussions in my small classes have been best\nZoom discussions.\nZoom doesn\u2019t work all that well because it cuts out frequently.\nZoom during normal class time.\nZoom for sure\nZoom for sure\nZoom has been best, but still is not the same. I do like the features for screen-sharing, chat, etc. MS Teams is horrible, and Panopto is good but is too asynchronous to be suitable long-term.\nZoom has been decent when we've used it, but it is a bit much to be asking students to be able to commit to classes during this time. Fortunately, the Psychology department has been very understanding of all of this.\nZoom has been difficult because it does not work well with large discussion based classes.\nZoom has been effective for most of my classes\nZoom has been good, able to see classmates and teacher just learn from screen\nZoom has been great because of the screen sharing ability for my lectures and for the video features for my discussion classes.\nZoom has been great!\nzoom has been more effective than recording classes.\nZoom has been working out great\nZoom has worked best but I am lucky to have efficient wifi\nZoom has worked fairly well. Microsoft didn't really work.\nZoom has worked fine\nZoom has worked well and kept me engaged, though it's very hard on the eyes sometimes.\nZoom has worked well most of the time.\nZoom is fine\nZoom is fine. It's hard to concentrate and becomes easy to disassociate while class even if the material is interesting.\nZoom is good and reliable.\nZoom is good. I hate online class as a concept, but the software itself is very good.\nZoom is really helpful for going to office hours or TA hours. I also liked Panopto because the professor can record themselves speaking and record the PowerPoint, which is nice.\nZoom is way better than pre-recorded lectures.\nZoom is working just fine to be honest.\nzoom lectures\nZoom lectures\nZoom lectures\nZoom lectures\nZoom lectures\nZoom lectures are pretty hard to focus on sometimes, especially if the professor gets sidetracked a lot. It's easier when there are a lot more breaks in class--not breakout groups, but changes of media like a video vs notes, etc Having the same structure of class as before is really helpful since it is familiar and written problem sets are fine for me.\nzoom lectures/discussions\nZoom lectures/seminars are ok with me.\nZoom live courses\nZoom live meetings Recorded lectures\nZoom meeting\nZoom meetings\nZoom meetings\nZoom meetings\nzoom meetings, data analysis of professor conducted research\nZoom meetings.\nZoom recorded classes\nZoom recorded lectures\nZoom recordings have been useful\nZoom seminars\nzoom seminars I guess.\nZoom seminars in which students can interact with one another work best for me.  Zoom lectures are also good to attend synchronously since I can send questions to the professor in real-time, and their being recorded has been really helpful when I for some reason need to miss class.\nZoom synchronous meetings\nZoom virtual discussions.\nZoom works fine, however it is very hard to stay focused\nZoom works pretty well\nZoom works somewhat better than the asynchronous class (which is a Bryn Mawr one).\nZoom works very well. I find that synchronous meetings force me to stay more on top of my work and maintain a schedule.\nzoom!\nZoom, email\nZoom, for sure.\nZoom, Google drive, moodle\nZoom, I suppose.\nZoom, ie face to face instruction\nZoom, its hard to watch posted lectures.\nZoom, Moodle\nZoom, recorded lectures\nzoom, texts to read and quizzes to respond to\nZoom, video lectures.\nZoom.\nZoom.\nZoom.\nZoom.\nZoome discussions\nZoom-ish", "Q14: Of the online instructional methods that you have experienced, which ones have not worked well for you?\t\nI would say they've all worked, just to varying degrees.\nRecorded lessons\nI really dislike all of the methods.\nAsynchronous on-your-own assignments\nPosted lectures have been very helpful to revisit\nMoodle forums\nOther than zoom and usual moodle things, there isn't much else that I use.\nposted notes and homework\ntheyve all been fine\nThey\u2019ve all worked pretty well for me.\nI did not like recorded lectures.\nprofessors that just maintained old class structure\nAsynchronous lectures have not worked\nNot so much\nsticking to strictly what we were doing before but now online.\nI do not like when professors just give us documents to fill out rather than having a discussion.\nZoom is a little glitchy in larger classes.\nGoogle Teams\ni have no motivation to watch recorded lectures\nThe Powerpoints are fine for lectures but it can be difficult to find the time to watch them / simultaneously take notes. The process takes a bit longer than it would if the lectures happened in real time.\nAsynchronous classes, sort of\nSynchronous methods helped but were often set at a generic pace (working on example problems together). This meant that sometimes, classes were class unhelpful.\nSome group discussions are a little embarrassing, not that people don\u2019t want to talk. Just not sitting together makes discussion hard and less tangible. Hope professors could address this by involving more people in groups or lead better discussion topics.\nZoom is effective, but I hate it. There\u2019s no better solution though.\nZoom hasn\u2019t been very helpful.\nIf I were to pick a least favorite aspect of online class it would be having seminars over zoom.\nFor the lab that I am in, since we cannot have any subjects do our experiments, we were asking to just make up results and we haven\u2019t had class for the passed three weeks so it is hard to continue the motivation for this class.\nMicrosoft teams\nOne on one discussions, while very rare in the classes where they occur, have been somewhat less helpful.\nexpecting the same amount of effort and workload of students as before all of this\nCancelling class\nZoom office hours are intimidating Class participation via zoom\nActual class has worked fine. The harder part is completing work outside of class especially on the types of assignments I would\u2019ve been able to collaborate on and get TA/lab hours help with at school.\nit's hard to juggle so many different discussion threads across multiple classes\nClasses that are not having Zoom meetings and are only posting online readings and responses.\nPre recorded lectures\nBecause I don\u2019t have a printer at home I have a difficult time reading so much material online..\nEmails!  Also there are some professors who choose to not record office hours for specific reasons.\nsuper long classes (3 hrs)\nMoodle discussion boards\nZoom does not work well for me because my internet connection is not the best\nI am not a big fan of the prerecorded lectures\nZoom keeps giving me connectivity issues and freezing\nZoom, Voicethread.\nGroup projects and class discussions\nI sometimes have some issues with Zoom-- and I'm not a fan of the fact that I have to sit in front of a computer for so long everyday-- but in the long wrong, it isn't terrible, because at least I am lucky enough to be able to access zoom and attend my classes as usual\nFor one class we no longer meet as a group. There are activities and office hours but no more lectures.\nRegular lecture discussions because I don't want to or feel confident participating.\nIt\u2019s been okay so far, but zooming computer science lab is very challenging and I don\u2019t get a lot out of it\nrecorded lectures\nExpected attendance with lessons that could be recorded lessons instead\nThe only hard part for me is with my discussion classes because it is harder for me to participate because we are not raising our hands and we have to just jump in and since I am quiet that has been hard, so I have had to wait til nearer the end of class when the ideas are all already out.\nRecorded panapto lectures\nZoom\nSynchronous classes have been harder for more interactive types of class.\nZoom has been the main method and it is fine but the time difference and unusable WiFi network can be hard to adjust to.\nIt's been hard to research and also read many chapters of books online and focus and everything, but that's no fault of Haverford.\nPanopto, because the quality is not ideal and the course feels scattered.\nZoom at 6am\nthe moodle forums as a substitute for class has seriously harmed my learning experience and makes me feel as if I'm learning a lot less. I would rather a recorded lecture instead.\nNone\nmoodle and bionic (although we haven't used bionic thus far) are very very outdated pieces of software. Bionic especially is not intuitive at all and I imagine will be even worse once we start using it to choose classes shortly.\nI have found my zoom classes really hard. I have a lot of trouble following what is happening, and find it really easy to get distracted.\nNone of them are great\nIt can be difficult to participate in the zoom format, especially in larger courses or when some students take up space in discussions.\nZoom classes\npanopto\nNone\nLike I said, courses that have increased workload - primarily through weekly \"reflections\" - have proven really burdensome.\nMy one class is basically an entire powerpoint with each slide dedicated to a new exercise we are supposed to complete on our own from our textbook.\nSynchronous learning while on the west coast-- As mentioned before, waking up for certain classes is a challenge to me! I forgot to say earlier, but expectations of synchronous TA sessions are also really difficult me, as the normal 8PM PST session that is basically required to finish homework assignments for one class means I have to find a way to get out of dinner with my family. This is not always possible for me, as I am usually responsible for cooking and cleaning it!\nnone\nsynchronous meetings on zoom since all of my classes are early in the morning\nThere's not any in particular that haven't worked well for me.\nThey were ok\nThe synchronous sessions have not worked as well.\nAsynchronous lectures (pre-recorded).\nI think some of the Zoom breakout rooms aren't always very productive.\nI have not appreciated when professors just give readings and problems without much external instruction or clarification on materials. It makes it unclear what I have to learn and leaves learning up to a bunch of confusion (and an apparent lack of motivation).\nNone (the asynchronous model works alright, just less well than Zoom).\nThose that are not flexible (see above).\nI don\u2019t like synchronous lectures.\nZoom and moodle discussion boards. I like zoom and I think it would work extremely well if I had my own bedroom in my house or had 4 less people living with me, but my house is too crowded and noisy to really make zoom work, Plus, my internet isn\u2019t fast enough so I spend most of class staring at a frozen screen.\nAll have worked for me.\nAll of them. Professors need to practice and learn how to make online learning effective. If I were to show up to my thesis talk without having practiced and it was a mess, that would be on me. Similarly, professors not practising to engage students digitally is on them. Recognizing the difficulty of learning said skills, the professors are trying; but, the quality of education drops significantly\nTeachers trying to lecture as if we are in a classroom\nMicrosoft as the professor is only using voice, not visual so it\u2019s difficult to follow along\nLive zoom classes have been hard\nmy professors who have not really done anything but have us submit work via email\nzoom lectures\nDiscussions\nZoom.\nSynchronous\nMoodle discussion forms\nSynchronous lectures\nZoom?\nUploaded material for self-teaching\nOnes that have expected the same of me.\nI have a class where we have a group project, which has been frustrating\nI still don't know what instructional method means\nMoodle.\nZoom\nonline but students are all muted/video turned off\nThe posted lectures.\nOne downside of synchronous lecture is that there is sometimes trouble maintaining a strong enough internet connection to \u201ccatch\u201d everything that professors and classmates say.\nForced class discussion\nMostly, my classes have worked out fine, although our discussion groups haven't been super effective.\nAll have worked well\nThe Zoom classes are just hard to be attentive too. You can't be more removed from a class setting than being a couple miles away from your professor and on you laptop. Students at Haverford are driven to do their work but its really hard when theres so many distractions and its hard to be involved in class online. I think having prerecorded classes allows students to do their work before deadlines because they can complete it on their own time and they are zoned in because at 1 am if I want to watch my psych lecture Im doing it because I'm focused productive and ready to watch all hour and 15 of it.\npre-recorded lectures, it does not capture the same interactive environment, and i imagine is just as weird for the profs as it is for us.\nPre-recorded lectures.\nZoom classes where people aren't comfortable asking questions are the worst.  Also I know in many breakout rooms I've been in or received snapchats of, people don't have their camera on, and are on mute.\nChemistry Question Center\npanopto, zoom presentations\nGroup projects analyzing laboratory data  Revising the grant Online discussion boards\nDefinitely the synchronous lectures, but it depends on course content\nNone.\nLectures, when pre-recorded, have been effective, although when these are carried out remotely and synchronously, they can be more difficult to access, and there can be less room for flexibility in the discussions/interactions between instructor and student in these situations\nAll have worked .\nlecture\nSometimes individual meetings with professors..\nI think video lectures are more of a struggle for me, but I think it\u2019s just because of the need to actually make myself focus. However, I believe they\u2019re necessary for earlier classes.\nSome professors have attempted to maintain the same syllabus or courseload given the crisis(especially when these clases were lab based or already intensive). It is extremely hard to memorize and conceptualize parts of the brain and neurology through a zoom call.\nOnly having recorded lectures\nSynchronous meetings are also somewhat problematic, because time zone changes make these difficult to attend and do my best work in.\nThough I see the advantages of asynchronous learning, I think it has not worked as well for me.\nAsynchronous learning.\nLectures- they just feel draining. I don\u2019t feel like I\u2019m paying attention.\nMeeting in small groups at non class times and reporting back to the professor. I understand the value of small group work and have appreciated doing it as part of class time using the zoom breakout groups.\npowerpoints in non-lecture classes small discussions where the professor dominates the entire discussion\nGiven the circumstances we find ourselves in, I think it would be harsh to say that some online instructional methods haven't worked outright. Everyone's trying their best. Successful/unsuccessful instructional methods are more dependent on the type of class being taught.\nZoom lectures.\nI have not particularly enjoyed the various asynchronous discussion forums I have used, like VoiceThread, Moodle, Slack, etc.\nSmaller, more frequent assignments. They are simply very difficult to keep track of and - even if they are not assessed as late now - frequently realizing you have forgotten something is another nagging sense.\nmoodle\nthey have all worked well for me because different classes require different methods and teaching styles\nKeeping the same dates. Keeping the exact same projects/ assignments due without requiring less of us. Expecting us to give this all of our attention like we don\u2019t have other things going on in our lives.\nmoodle overall slightly annoying to use\nRecorded lectures\nSynchronous lectures have worked decently when in the afternoon, but when they're in the morning I struggle to attend and pay attention.\nZoom has been a little tricky with time difference but otherwise fine.\nResources like the CQC and office hours have been a little bit difficult to deal with because there is less structure and often times a lot of people sign on.\nZoom\nPanopto\nI guess zoom?\nRecorded lectures.\nonline lectures, harder to learn and I feel disconnected\nNone have been that bad\nNone so far.\nAsynchronous lectures that have class material, homework, and larger assignments all due Sunday nights.\nNone\nMicrosoft teams was very difficult to operate.\nIn my bigger class, Zoom discussions were hard.\nRecorded lectures are fine, they just lack the social aspect and ability to ask questions.\nAsynchronous learning through a combination of recorded office hours and lectures from past years has been difficult to follow.\nEngaging in class discussion on twitter.\nGroup projects (presentations) are very time consuming and in my opinion not very logical in this kind of settings. Smaller the groups the better.\nMicrosoft Teams was hot garbage\nZoom class meeting\nSynchronous meetings. Also, my chem class has a lot of workload now compared to before and it's very hard getting the support I need\nPre-recorded powerpoints. I wish I could speed up the audio; I don't want to spend an hour listening to information I could digest in half an hour.\nOnline lectures where our cameras and mics were off are very difficult for me as I have focus problems and without any external incentive it's very difficult to pay attention.\npiazza\nAsynchronous lectures\nMoodle forum\nAgain, zoom and other similar video chat platforms just feel exhausting, in the sense that I'm never sure how to balance my own interjections and others'.\nOnly applicable when internet is slow or down\nIt's really hard to focus without being in the classroom. In my CS classes, the physical/social lab space is really important (I've learned this by suddenly not having it).\nZoom lectures  Recorded lectures\nsynchronous lectures, breakout rooms/discussion in large lectures\nI wouldn't say that any of them have worked particularly poorly, but purely lecture based classes have been less effective, since I no longer have the opportunity to casually discuss their content with my classmates.\nThe zoom office hours.\nThe Microsoft teams meetings without visual aids or video have been terrible to follow\nLarge group discussions.\nPizza for my Bryn Mawr class.\nRecorded lectures are helpful in that I can pause when my professor goes to fast, but also difficult in that nobody can ask questions during lecture.\nThey've all worked.\nAsynchronous formats like reading assignments and essays (without meeting for class) have not worked well for me as I find myself struggling to engage and really understand the material. While my professors have made themselves very available, it is simply not the same as asking them questions in real time, and also engaging with the questions of my peers, something I find helps with my own learning.\nThe flipped classroom in physics has made it much harder to motivate myself to do work.\nSynchronous unrecorded classes have been difficult to keep up with.\nArt is kind of hard because you cannot really see everyone else's progress, and it is hard for instructors to offer advice on out paintings.\nMicrosoft teams caused many issues in my language class bc of sound issues\nLong form open ended projects. Two of my classes have a final project that we've shifted focus to, and I\"m very worried I just straight up won't do them. I've got a first draft due in two days and still need to convince myself to reread the paper its about.\nRecorded lectures on Panopto. They have been hard to follow.\nN/a: all have been fine\nBig essay assignments\nBusiness as usual classes are not realistic. Reductions in scope of the class or other forms of added flexibility seem very necessary to me\nMorning classes via Zoom.\nThe tests have been a little bit weird in terms of format. Since they're just like attach in an e-mail or on Moodle.\nNIL\nSynchronous lectures. Especially if we are expected to attend all of them.\nLive classes\nLecture recordings\nI am really falling behind in the class that is completely just readings, then writing a 2 page response, and having all my responses due in late April.\nProfessors from study abroad not posting lectures for 3 weeks straight.\nNot applicable as zoom is the only way my professors have been teaching.\nNone. Zoom classes are fine, but then again I don\u2019t have anything that\u2019s heavily action based so I\u2019m lucky.\nZoom lectures with 10+ people.\nThey have all worked relatively well.\nthe complete asynchronous method because without face to face teacher guidance it is easy to get off track and harder to know the expectations for each assignment.\nthey are all working okay\nThose that still have stringent deadlines or strict methodology.\nVideo lectures.\nSlack\nThe elephant in the room is that online learning just doesn't work for Haverford? I am not learning anything from any of my classes, except my thesis which has continued about the same as when I was on campus. All my friends share the same sentiment. Given the circumstances, I'm OK with that, and personally I think the college and its professors should focus more on supporting students emotionally than trying to continue like normal with teaching. In addition, several professors of my friends have flat out said that they plan on giving everyone a 4.0 for the semester, which doesn't exactly inspire further work or motivation to learn.\nLinear algebra as a live zoom class feels like an inefficient use of my time. It's always a lecture so I don't understand why we can't have it recorded and for me to look at any time.\nZoom breakout discussion rooms\nThe synchronous classes with regular meetings have caused a lot of stress and exhaustion, especially because they are both 2 hour 30 minute classes which meet on the same day.\nRecorded lectures. There just isn't that much accountability to complete them, and it feels pretty boring and dry to stare at your professor on a computer screen for an hour.\nBreakout rooms and requiring additional participation outside of class through Moodle forums\nThinking that I can do as well as I would be if I was at school. My thesis has been the exact same and now feels even more strenuous without the resources I had at school.\nNot Applicable\nThe classes that require more lecture based instruction.\nI dislike recorded lectures the most\nI have one class where, in lieu of class, we have just been submitting short essays on the reading. I have personally found it difficult to complete work of this nature, so I'd much prefer to have more task-oriented or conversation-oriented assignments.\nI personally don't learn with online methods.\nAssignments of the same volume that is normally expected of a typical semester at Haverford are too difficult to achieve given that staring at a computer for 10+ hours a day and family responsibilities are major sources of stress.\nWatching videos ahead of time and then attending Zoom hours to ask questions. I am not going to wake up to join Zoom hours at 6:30am to ask questions.\nVoicethreads has been difficult to figure out and creating videos is awkward. Google hangouts were bad because they were kicking students off the class, but we then switched over to zoom and that's been fine.\nPanopto-recorded lectures have been the most difficult.\nMoodle forum discussions.\nOptional learning. I just don't do it, even if it would benefit my educational experience. Also, one of my classes used to be on Microsoft Teams, and that didn't work.\nself-managed textbook reading and supplemental videos\nZoom and lecture recordings\nThis method works as well as you'd expect. I'm learning but it's incredibly boring and demotivating to not be able to interact while watching a lecture and I'd much prefer recorded live lectures that others could watch later.\nI haven't had a direct issue with this (because of panopto recordings) but I think synchronous learning may be very difficult and unfair to some students because of where they are.\nI find it harder to actually commit to fully learning in an asynchronous class. But, the class that has worked worst for my learning is the synchronous meetings that are audio only and I am just watching a screen that says my professor's name on it.\nI wouldn't say that any haven't worked well, although I preferred reading and powerpoint instruction less.\nlive zoom lectures, prerecorded panopto lectures\nLectures are unengaging.\nnone\nZoom is effective and I believe is the best option\nLive Zoom sessions with more than 10 people. I\u2019m in a class where there are routinely more than 25 participants and with an online connection that can be a bit temperamental, it becomes frustrating when trying to have an efficient conversation and let everyone participate (which the instructor expects).\nSometimes I have difficulty connecting with Zoom, but the class is posted afterwards if I need to rewatch.\nSynchronous online meetings through Zoom are not working as well for me. It is difficult for some members of our classes to access Zoom at specific times. It really changes the class dynamic and the discussions when not all members of the class are able to participate as they normally could. Class is also significantly less engaging when there are connectivity issues or glitches/lagging in Zoom that result in missing part or all of what someone just said\nI find it tricky to do long readings at home. My concentration is not the same. I prefer short, compact information.\nN/A -- all of my professors have done a good job\nOne of my professors emailed us a list of assignments to complete by the end of the semester, and that confused me at first because I didn't realize initially that that was all they were requiring (i.e. that there were holding no synchronous classes).  Now it's been hard to motivate myself to gradually complete all the assignments, even though I enjoy the material.\nnormal class hours with zoom didn't work well because the Wifi in the BCC is terrible and I could not maintain connection\nIt is incredibly unclear what is due, when it is due, and how to submit it.\nSame as what I said above.\nI do NOT like traditional lectures directly transposed into zoom.\nI do not like voice-over powerpoints.\nLarge Zoom classes have honestly been painful because it's really hard to be engaged in this virtual setting when you can barely see the 30 other people in the class. Sometimes asynchronous learning doesn't work very well either (depends).\nOnly readings and posted videos\nHaving class over zoom is just not productive. People don't listen / attend lectures always and hard to have class in your home\nWriting response papers to readings\nI haven't felt like any of them have been working very well, it's been very difficult to engage.\nmoodle discussion forum!\nPrerecorded lectures, pre-made data sheets for labs\nIn one class, the readings have become mostly optional, and that hasn't worked for me because then the discussions are ineffective. I still want some responsibilities and semblance of normality. I know from other classes that it is still ok to expect something of me.\nWhile I appreciate the attempt to recreate the social interactions of a classroom via live Zoom classes, my environment just does not allow me to do it effectively.\nLARGER ZOOM seminars\nZoom office hours and Moodle forums.\nNothing in particular.\nThey've all worked pretty well\nMS Teams, Panopto.\nComplete asynchronous learning\nI think lectures aren't engaging over zoom and asynchronous methods don't provide any instruction form professors (although those are the preferred methods of many professors).\nPre-recorded lectures are not effective at all.\nBreakout rooms on zoom\nPosting of Lecture slides without walkthrough.\nWhile I don't have any specific grievance with Zoom, the problem is the time zone change which is the biggest problem in adjusting my schedule.\npanopto recordings\nzoom is honestly somewhat disturbing and I've been staring at screen literally 24/7.\nzoom sometimes crashes\nZoom meetings for seminar-based courses are more difficult\nOnline discussion forum\nLarge group zoom discussions are much more intimidating to engage in than smaller discussion groups.\nZoom meetings\nnone\nZoom's Breakout room\nPre-recorded lectures and communication over slack.\nLearning online is difficult in general & I don\u2019t think I\u2019m doing very well in most of my classes but I\u2019m still putting in as much effort as I was before. I think a lot of it has to do with the fact that the material is hard & is not meant to be taught online & the translation is struggling.\nFor the most part, all the online instructional methods have worked well for me.\nSynchronized learning can be very beneficial to me, but sometimes it cost for a lot of anxiety. I am not sure why probably because it\u2019s the closest thing to accountability that is required of me at this moment.\nZoom seminar\nLab videos don't convey the experience of doing a lab at all\nI am not sure.\nblog posts and optional zoom\nrecorded lectures.\nUploaded lectures\nAsynchronous work has not worked well for me.\nMoodle forums and writing responses\nThe Moodle discussion board is a horrible way to conduct class. It is difficult to follow and impossible to hold a conversation.\nPowerPoints posted on Moodle without synchronous class discussion or even a recorded teacher lecture.\nMeh everything works half decently. I don't think any of them are great or particularly desirable or comparable to in-person instruction.\nI don't think any of them didn't work for me.\nClass discussion-based courses that have been synchronous. I find it harder to be inclined to speak on zoom, only a few people do all of the talking every class.\nvoice threads the most, but also small group discussions\npre-recorded powerpoint presentations.\nSynchronous lecture\nOne thing I would wish for generally is to have more breaks during these online classes so that I do not have to sit down hunched over my computer for so much consecutive time.\nIt has been challenging for me to follow along with lectures over zoom.\nA synchronous lectures\nIn my discussion heavy film studies course, it has become difficult to recreate the setting through Zoom, which we had in class.\nSome of the asynchronous materials, such as posting just powerpoint without video instruction, is not optimal.\nObviously the lack of in-person help is much different than the online version of office hours/TA sessions. Mainly for me, it is hard to be motivated/remain focused in a different environment without my peers.\nprobably excessive zoom meetings- once per week or so for a class is good, but classes that have several I just find myself not feeling very engaged sometimes\nThey all worked out quite well.\nFull zoom classes are tough, I usually have to turn my video off and clean the kitchen or something bc otherwise I can\u2019t focus. But then I feel like professors think I\u2019m not actually paying attention which is frustrating. Also trying to write long essays for a grade right now feels like that myth about the guy pushing a rock up a hill over and over\nI dislike zoom because of my connection issues.\nPre-recorded lectures, group activities (as everyone is in different timezones etc.)\nI don't have any major problems with asynchronous classes, I just don't like it as much as the synchronous classes. Also, this isn't due to any specific tool, but I've found painting/fine arts classes to be much harder to do online.\nZoom.\nScreen sharing whiteboards\nAll of my classes are meeting on zoom.\nI don't really think I've used anything other than Zoom, except Google Hangouts to talk to a prof. during office hours. That was fine.\nMoodle\nvideos without synchronous class time\nBoth work well in their situations.\nRecorded lectures, lectures without visual cues.\nI bet online classes dont work for international or west coast sTudents\nOne thing I don't like with Zoom is that unless your laptop is touch-screen, it can be difficult to show your written work to someone else because the whiteboard feature on Zoom can be difficult to write on. I also didn't like the moodle chats because you have to type everything instead of saying it, which I think is more efficient.\nNone\nZoom lessons for lectures that could be pre-recorded.\nDiscussions don\u2019t work well on zoom. Everyone just mutes or doesn\u2019t talk. Good for lectures I guess but none of my classes this semester are lectures\nRecorded lectures.\nSometimes the breakout rooms are frustrating because the professor will be in a certain \"room\", which has a longer conversation. The other rooms do not have as much to talk about and once they finish their discusses just wait for the professor to pull everyone back to the main session. This feel like a waste of time.\nRecorded classes\nRecorded Zoom\nConstant discussion forums on Moodle feel really redundant and unimportant sometimes.\nNone\nOffice hour feels more complex.\nNothing in particular except rigid deadlines make things difficult.\nAsynchronous with no video lectures\nI don't think anything has not worked for me because I am flexible and adaptive.\nNon-synchronous work\nRecorded videos, panopto lectures.\nAsynchronous learning in all forms has been rather unhelpful because it becomes more difficult to engage with the material and asking questions becomes far more difficult. It seems to also just add to an already rather heavy workload.\nRecorded lectures and written discussion\nstraight lecture\nBlog posts are just busy work; bur I guess you need to make sure we\u2019re actually doing the readings. My history zoom classes are not good.\nUnsynchronized class is really impersonal. It's hard to collaborate with other students and/or the professor.\nno\nZoom Class Meetings\nZoom\nZoom lectures\nNone\nSynchronous lectures\nNone have been outstandingly unproductive.\nI\u2019m not sure what you mean by \u201conline instructional methods\u201d\nThe pre-recorded lectures\nTeams caused problems for my French class (at BMC). We spent more time reconnecting than having actual class. We have recently moved to Zoom\nI haven't enjoyed the student power point presentations. Lectures online are also more difficult to pay attention to.\nSlack and Moodle\nZoom worked well\nThere hasn't been anything that I find particularly bad. Sometimes in live Zoom lectures I find it difficult to participate and interject yourself into the conversation- it is a bit awkward and cumbersome to need to constantly mute/unmute yourself, and there is no real way to effectively get the professors attention besides just blurting something out in the middle of their lecture.\nMeeting once a week for discussions as opposed to twice. This really makes me feel more distant from the course and interrupts the rhythm of the class. That being said, I have a class that does not meet at all but has assignments due twice a week that has been going well.\nPanapto. It is very difficult to be manage the times to watch the lectures while taking care of things at home.  Zoom. It is hard to see and hear everyone when my wifi is not stable.\nLecture Recordings\nI haven't been as huge a fan of the online meetings via zoom, since structuring classes as though we are able to meet in person and conduct the lesson as though we werent thousands of miles apart is not working.  Making it based on assignment completion and posting (with the option for doing a zoom meeting purely as a freeform, unstructured discussion of the material for those able and interested) has been much easier for me as of now.\nBoth. See above.\nLabs are pretty sad--it's not good just analyzing data.\nThey have all been OK, none has been particularly bad.\nNone of the programs have not worked well for me.\nNone!\nUsing lectures that had been recorded from last year\u2019s classes\nThe lectures have been the least effective.\nOffice hour\nThey have all been helpful.\nIt hasn't hindered my learning at all, but I pretty much ignore lecture recordings if there are other materials with the same information\nLarge assignments with flexible due dates\nOnline discussions feel very superficial and the a-synchrony of it takes a lot away from the richness of discussion\nNone of them.\nThe class without a lecture did not work well, and the class with ambiguity around day-to-day reading assignment, did not work well for me at all.\nMeeting for class time to discuss (though it is a seminar class)\nEven though its somewhat effective, I still struggle with Zoom. I just find it way more challenging to pay attention online\nJust overall, the stress of the situation and of disconnect from Haverford leads to low motivation, engagement, and interest\nOnly Question and Answer sessions which people do not show up to have been mediocre.\nSince the lectures are not written on multi-layered blackboards, it's hard to refer to the previously written information. Also, sometimes I can't write everything I need.\n3.5 hour zoom courses will be the death of me! This happened twice in two separate once a week courses. Cannot do that again.\nBiology sucks with online seminar and lab.\nI have not enjoyed discussion forums, I think they become bland and repetitive very quickly.\nonline readings\nI only used zoom\nAsking for group presentations or other types of work that heavily depends on group dynamics has been really hard online\nWatching lecture recordings was difficult. Synchronous learning with a class of 30 for a discussion class was not good. It was very hard to participate, especially since the participation grade remained.\nPiazza\nZoom classes\nAll have been fine\nWatching labs and then writing as normal\nTo be very honest, I dislike virtual learning a lot. It is very incompatible with me, so I would say all of them have not worked well for me.\nI wouldn't say zoom lectures did \"not\" work, but they were just harder to access and participate in.\nSee above.\nThey have all worked.\nI think the regimented nature of the life classes was better than the flexible nature of the pre-recorded classes because it is easy to slack off at home\nlong classes with presentations\nTrying to collaborate on whiteboards with other students in small groups has been hard.\nBoth of them.\nI took a CS class at Bryn Mawr and the professor disappeared for over a month and only gave one lecture after spring break (during the last week of class)\nAsynchronous learning and discussions threads have not worked for me.\nI don't love moodle posts being the basis of class interaction and participation personally, but they're okay.\nOnline lectures\nI don't believe that Zoom classes should be synchronous mandatory. I don't think that is fair for everybody.\nmy painting class was done online, which was not very necessary, but not problematic. I would suggest that the teacher just had office hours.\nNone in particular\nI do not have an answer.\nI really struggle to pay attention in zoom lectures\nyoutube videos. i did not pay this much money to have the internet teach me\nOnline group work.\nPasting from \"For your current term online courses, please list which instructional methods have been used.\" real time zoom discussions readings essay writing moodle discussions audio files zoom lectures\nHaving to do the work of college at all during this time has not worked particularly well for me, and it's overall felt like a shell of the previous experience. Mostly though I'm just a little frustrated that Haverford felt the need to make seniors finish the semester during this ridiculous global pandemic.\nstudy abroad class\nPre-recorded classes.\nNone of them\nSynchronous class meetings through zoom\nlike I said, they have been fine, but hardly adequate"]}}; }
plotInterface = buildViz(1000,600,null,null,false,false,false,false,false,true,false,false,true,0.1,false,undefined,undefined,getDataAndInfo(),true,false,null,null,null,null,true,false,true,false,null,null,10,null,null,null,false,true,true,undefined,null,false,false,".3f",".3f",false,-1,true,false);

autocomplete(
    document.getElementById('searchInput'),
    plotInterface.data.map(x => x.term).sort(),
    plotInterface
);

</script>