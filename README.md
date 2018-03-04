# jQuery Bus Seat Boking

### jQuery Seat Charts (JSC) is a full-blown seat map library. It will generate an accessible map, legend, handle mouse & keyboard events and finally give you powerful selectors to control your map.

[Simple demo map](http://jsc.mm-lamp.com/)

## Example:

Basic setup:

	$(document).ready(function() {
	
		var sc = $('#seat-map').seatCharts({
			map: [
				'aaaaaaaaaaaa',
				'aaaaaaaaaaaa',
				'bbbbbbbbbb__',
				'bbbbbbbbbb__',
				'bbbbbbbbbbbb',
				'cccccccccccc'
			],
			seats: {
				a: {
					price   : 99.99,
					classes : 'front-seat' //your custom CSS class
				}
			
			},
			click: function () {
				if (this.status() == 'available') {
					//do some stuff, i.e. add to the cart
					return 'selected';
				} else if (this.status() == 'selected') {
					//seat has been vacated
					return 'available';
				} else if (this.status() == 'unavailable') {
					//seat has been already booked
					return 'unavailable';
				} else {
					return this.style();
				}
			}
		});
	
		//Make all available 'c' seats unavailable
		sc.find('c.available').status('unavailable');
		
		/*
		Get seats with ids 2_6, 1_7 (more on ids later on),
		put them in a jQuery set and change some css
		*/
		sc.get(['2_6', '1_7']).node().css({
			color: '#ffcfcf'
		});
		
		console.log('Seat 1_2 costs ' + sc.get('1_2').data().price + ' and is currently ' + sc.status('1_2'));
	
	});


## Basics:

Building maps is fairly easy with jQuery Seat Charts, you can literally pass an array of strings which represents succeeding rows. Let's take a look at a theatre example:

	//Seat map definition
	[
		'aaaaaa__DDDDD',
		'aaaaaa__aaaaa',
		'aaaaaa__aaaaa',
		'bbbbbb__bbbbb',
		'bbbbbb__bbbbb',
		'bbbbbb__bbbbb',
		'ccccccccccccc'
	]

Each single character represents a different type of seat and you have a freedom of choosing anyone but underscore **_**. Underscore is used to indicate that there shouldn't be any seat at a certain place. In our example I chose **a** seats to be the closest to the screen, **D** meant for disabled and **b** and **c** as just plain seats. I also built a corridor in the middle of our theatre, so people can conviniently reach their seats.

Your chosen characters can carry a hash of data which is a great way to pass crucial seat details such as price or a description that you want to show on hover.
 
	seats: {
		a: {
			price       : 24.55,
			description : 'Fair priced seat!'
		}
	}

Once you build your map and define seats, you can start implementing the booking magic.



