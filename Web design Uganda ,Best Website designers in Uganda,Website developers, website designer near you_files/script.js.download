/*--------------------------------------------------------------
 Custom js
 --------------------------------------------------------------*/

jQuery( document ).ready( function( $ ) {
    'use strict';

    // Tooltip
    $('[data-toggle="tooltip"]').tooltip();

    // Search in menu
    var $search_btn = $( '.header-search > i' ),
        $search_form = $( '.header-search .search-form' );

    $search_btn.on( 'click', function() {
        $search_form.toggleClass( 'open' );
    } );


    // Scroll Animation
    var wow = new WOW({
        boxClass:     'wow-animation',
        animateClass: 'animated',
        offset:       0,
        mobile:       true,
        live:         true
    });
    wow.init();

    // Mobile Menu
    $('.mobile-menu .mobile-menu-toggle').on('click', function () {
        $(this).parent('.menu-item').toggleClass('open');

        return false;
    });
    $( ".mobile-search" ).on( "click", function() {
        $( "#search-mobile-toggle" ).toggle(200);
    });

    // Search
    var $searchContainer = $( '.full-screen-search-container ');
    $( '#js-search-overlay' ).on( 'click', function ( evt ) {
        evt.preventDefault();

        $searchContainer.addClass( 'open' );
        $searchContainer.find('.search-field')[0].focus();
    } );
    $searchContainer.on('click', function (evt) {
        if (!$(evt.target).parents('.search-form').length) {
            evt.preventDefault();

            $searchContainer.removeClass( 'open' );
        }
    });

    // Fitvids
    $( ".container" ).fitVids();

    // Post Gallery
    $( ".post-gallery" ).slick({
        dots: true,
        infinite: true,
        arrows: false,
        speed: 500,
        adaptiveHeight: true
    });

    // Counter
    if ($.fn.waypoint) {
        $('.counter-container').waypoint(function () {
            var $this = $(this);

            if ($this.data('waypoint-run')) {
                return;
            }

            var $counter = $(this).find('.counter'),
                value = $counter.data('value'),
                decimalCount = value.toString().split('.'),
                duration = $counter.data('speed'),
                separator = $counter.data('separator'),
                decimalPoint = $counter.data('decimal');

            if (decimalCount[1]){
                decimalCount = decimalCount[1].length - 1;
            } else {
                decimalCount = 0;
            }

            var counter = new CountUp($counter.attr('id'), 0, value, decimalCount, duration, {
                separator : separator,
                decimal : decimalPoint
            });

            counter.start();

            $this.data('waypoint-run', true);
        }, { offset: '85%' });
    }

    // Testimonial
    $('.testimonial-container').each(function () {
        var $testimonialContainer = $(this);

        $testimonialContainer.find('.testimonial-list').slick({
            slidesToShow: $testimonialContainer.data('items'),
            slidesToScroll: $testimonialContainer.data('items'),
            mobileFirst: true,
            fade: ($testimonialContainer.data('items') == 1) ? true : false,
            dots: $testimonialContainer.data('dots') ? true : false,
            arrows: $testimonialContainer.data('nav') ? true : false,
            prevArrow: '<i class="fa fa-chevron-left slick-arrow-prev"></i>',
            nextArrow: '<i class="fa fa-chevron-right slick-arrow-next"></i>',
            autoplay: $testimonialContainer.data('autoplay') ? true : false,
            responsive: [
                {
                    breakpoint: 1024,
                    settings: {
                        slidesToShow: 2,
                        slidesToScroll: 2,
                    }
                },
                {
                    breakpoint: 0,
                    settings: {
                        slidesToShow: 1,
                        slidesToScroll: 1
                    }
                }
            ]
        });
    });

    // Promo Popup
    if (saturnthemes_financebank_params.promo_popup_show == 1) {
        var cookieKey = 'promo_popup_hide',
            hidePopupRegex = new RegExp(cookieKey + '=1');

        if (!hidePopupRegex.test(document.cookie)) {
            $.magnificPopup.open({
                items: {
                    src: '#promo-popup',
                    type: 'inline'
                },
                removalDelay: 300
            });
        }

        $('#promo-popup-checkbox').on('click', function () {
            if ($(this).prop('checked')) {
                document.cookie = cookieKey + '=1;expires=1;path=/';
            } else {
                document.cookie = cookieKey + '=0;expires=1;path=/';
            }
        });
    }

    var $window = $( window );
    // Scroll up
    var $scrollup = $( '.scrollup' );

    $window.scroll( function () {
        if ( $window.scrollTop() > 2500 ) {
            $scrollup.addClass( 'show' );
        } else {
            $scrollup.removeClass( 'show' );
        }
    } );

    $scrollup.on( 'click', function ( evt ) {
        $( "html, body" ).animate( { scrollTop: 0 }, 600 );
        evt.preventDefault();
    } );

    var $quantityContainer = $('.quantity-container');
    if ($quantityContainer.length) {
        $quantityContainer.find('.quantity-up, .quantity-down').on('click', function () {
            var $input = $quantityContainer.find('input'),
                step = $input.data('step'),
                min = $input.data('min') || 1,
                max = $input.data('max'),
                value = parseInt($input.val());

            if ($(this).is('.quantity-up') && (!max || max >= value + step)) {
                value += step;
            } else if ($(this).is('.quantity-down') && (min <= value - step)) {
                value -= step;
            }

            $input.val(value);

            return false;
        });
    }

    // Masonry
    if ($('.post-masonry-layout').length) {
        var $grid =  $('.post-masonry-layout').masonry({
            itemSelector: '.post-masonry-item',
            columnWidth: '.grid-sizer',
            percentPosition: true,
            gutter: 30,
        });

        $grid.imagesLoaded().progress(function() {
            $grid.masonry('layout');
        });
    }

    // Pie Chart
	function VcChart(element, options) {
		this.el = element, this.$el = $(this.el), this.options = $.extend({
			color: "#f7f7f7",
			units: "",
			label_selector: ".vc_pie_chart_value",
			back_selector: ".vc_pie_chart_back",
			responsive: !0
		}, options), this.init()
	}

	VcChart.prototype = {
		constructor: VcChart, _progress_v: 0, animated: !1, init: function () {
			this.color = this.options.color, this.value = this.$el.data("pie-value") / 100, this.label_value = this.$el.data("pie-label-value") || this.$el.data("pie-value"), this.$wrapper = $(".vc_pie_wrapper", this.$el), this.$label = $(this.options.label_selector, this.$el), this.$back = $(this.options.back_selector, this.$el), this.$canvas = this.$el.find("canvas"), this.draw(), this.setWayPoint(), !0 === this.options.responsive && this.setResponsive()
		}, setResponsive: function () {
			var that = this;
			$(window).resize(function () {
				!0 === that.animated && that.circle.stop(), that.draw(!0)
			})
		}, draw: function (redraw) {
			var radius, w = this.$el.addClass("vc_ready").width(), border_w = 10;
			w || (w = this.$el.parents(":visible").first().width() - 2), w = w / 100 * 80, radius = w / 2 - border_w - 1, this.$wrapper.css({width: w + "px"}), this.$label.css({
				width: w,
				height: w,
				"line-height": w + "px"
			}), this.$back.css({width: w, height: w}), this.$canvas.attr({
				width: w + "px",
				height: w + "px"
			}), this.$el.addClass("vc_ready"), this.circle = new ProgressCircle({
				canvas: this.$canvas.get(0),
				minRadius: radius,
				arcWidth: border_w
			}), !0 === redraw && !0 === this.animated && (this._progress_v = this.value, this.circle.addEntry({
				fillColor: this.color,
				progressListener: $.proxy(this.setProgress, this)
			}).start())
		}, setProgress: function () {
			if (this._progress_v >= this.value)return this.circle.stop(), this.$label.text(this.label_value + this.options.units), this._progress_v;
			this._progress_v += .005;
			var label_value = this._progress_v / this.value * this.label_value, val = Math.round(label_value) + this.options.units;
			return this.$label.text(val), this._progress_v
		}, animate: function () {
			!0 !== this.animated && (this.animated = !0, this.circle.addEntry({
				fillColor: this.color,
				progressListener: $.proxy(this.setProgress, this)
			}).start(5))
		}, setWayPoint: function () {
			"undefined" != typeof $.fn.waypoint ? this.$el.waypoint($.proxy(this.animate, this), {offset: "85%"}) : this.animate()
		}
	};

	$.fn.vcChat = function (option, value) {
		return this.each(function () {
			var $this = $(this), data = $this.data("vc_chart"), options = "object" == typeof option ? option : {
				color: $this.data("pie-color"),
				units: $this.data("pie-units")
			};
			"undefined" == typeof option && $this.data("vc_chart", data = new VcChart(this, options)), "string" == typeof option && data[option](value)
		})
	};

	$(".vc_pie_chart:visible").vcChat();
} );

// Override Pie Chart
window.vc_pieChart = function () {};

(function ($) {
    // Line Chart
    $.fn.saturnLineChart = function () {
        var waypoint = "undefined" != typeof $.fn.waypoint;
        return this.each(function () {
            function addchart() {
                $this.data("animated") || (chart = "bar" === $this.data("vcType") ? new Chart(ctx).Bar(data, options) : new Chart(ctx).Line(data, options), $this.data("vcChartId", chart.id), $this.data("chart", chart), $this.data("animated", !0))
            }

            var data, gradient, chart, i, j, $this = $(this), ctx = $this.find("canvas")[0].getContext("2d"), options = {
                showTooltips: $this.data("vcTooltips"),
                animationEasing: $this.data("vcAnimation"),
                datasetFill: !0,
                scaleLabel: function (object) {
                    return " " + object.value
                },
                responsive: !0
            }, color_keys = ["fillColor", "strokeColor", "highlightFill", "highlightFill", "pointHighlightFill", "pointHighlightStroke"];
            for ($this.data("chart") && ($this.data("chart").destroy(), $this.removeData("animated")), data = $this.data("vcValues"), ctx.canvas.width = $this.data('width') ? $this.data('width') : $this.width(), ctx.canvas.height = $this.data('height') ? $this.data('height') : $this.width(), i = data.datasets.length - 1; i >= 0; i--)for (j = color_keys.length - 1; j >= 0; j--)"object" == typeof data.datasets[i][color_keys[j]] && 2 === data.datasets[i][color_keys[j]].length && (gradient = ctx.createLinearGradient(0, 0, 0, ctx.canvas.height), gradient.addColorStop(0, data.datasets[i][color_keys[j]][0]), gradient.addColorStop(1, data.datasets[i][color_keys[j]][1]), data.datasets[i][color_keys[j]] = gradient);
            waypoint ? $this.waypoint($.proxy(addchart, $this), {offset: "85%"}) : addchart()
        }), this
    };

    window.vc_line_charts = function (model_id) {
        var selector = ".vc_line-chart";
        "undefined" != typeof model_id && (selector = '[data-model-id="' + model_id + '"] ' + selector), $(selector).saturnLineChart()
    };
})(jQuery);