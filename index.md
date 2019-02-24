<html>
  <head>
    <title>
      comp
    </title>
      <script type="text/javascript">
        function fetchGroups(url, cb, data) {
	if(!data) data = [];
	
	$.ajax({
		
		dataType:'jsonp',
		method:'get',
		url:url,
		success:function(result) {
			console.log('back with ' + result.data.length +' results');
			console.dir(result);
			//add to data
			data.push.apply(data, result.data);
			if(result.meta.next_link) {
				var nextUrl = result.meta.next_link;
				fetchGroups(nextUrl, cb, data);
			} else {
				cb(data);	
			}
		}
	});	
	
}

$(document).ready(function() {
	
	var $results = $("#results");

	$results.html("<p>Finding meetups with Ionic in the description.</p>");

	fetchGroups("https://api.meetup.com/find/groups?&photo-host=public&page=50&text=ionic&sig_id=2109318&radius=global&order=newest&sig=ad335a79ccce2b1bb65b27fe10ea6836305e5533&callback=?", function(res) {
		console.log("totally done");
		console.dir(res);	

		var s = "";
		for(var i=0;i<res.length; i++) {
			var group = res[i];
			s += "<h2>"+(i+1)+" <a href='"+group.link+"'>"+group.name+"</a></h2>";
			if(group.group_photo && group.group_photo.thumb_link) {
				s += "<img src=\"" + group.group_photo.thumb_link + "\" align=\"left\">";
			}
			s += "<p>Location: "+group.city + ", " + group.state + " " + group.country + "</p><br clear=\"left\">";
		}
		$results.html(s);
		
		
	});
		
});
        var queryString = window.location.search.slice(1);
        // if query string exists
        if (quertString) {
        qString = queryString.split('q=')[1].split('&')[0];
        alert(qString);
        }
        $.ajax({
  url: "https://api.meetup.com/Basel-NET-User-Group/events",
  jsonp: "callback",
  dataType: "jsonp",
  data: {
    format: "json"
  },
  success: function(response) {
    var events = response.data;
  }
});
        (function () {
  var module = angular.module('app', []);

  module.controller('MeetupEventsController', ['$scope', '$sce', MeetupEventsController]);

  MeetupEventsController.$inject = ['$scope', '$sce'];

  function MeetupEventsController($scope, $sce) {

    var vm = this;
    vm.Events = [];
    vm.scope = $scope;
    vm.loaded = false;

    vm.Refresh = function() {
      $.ajax({
        url: "https://api.meetup.com/Basel-NET-User-Group/events",
        jsonp: "callback",
        dataType: "jsonp",
        data: {
          format: "json"
        },
        success: function(response) {
          var events = response.data;

          for (var i = 0; i < events.length; i++) {
            var item = events[i];

            var eventItem = {
              Id: i,
              DisplayName: item.name,
              Description: $sce.trustAsHtml(item.description),
              Location: item.venue.name + " " + item.venue.address_1 + " " + item.venue.city,
              Time: new Date(item.time).toLocaleString(),
              Link :item.link,
            };
            vm.Events.push(eventItem)
          }
          vm.loaded = true;
          vm.scope.$apply();
        }
      });
    };
    function activate() {
      vm.Refresh();
    };
    activate();
  };
})();

      </script>
      </head>
    <body>
      <div class="row" ng-repeat="model in vm.Events track by model.Id" ng-cloak>
  <a href="" target="_blank" title="Öffnen auf meetup.com"><h3></h3></a>
  <label>Datum und Uhrzeit</label>
  <p></p>
  <label>Description</label>
  <div ng-bind-html="model.Description"></div>
  <label>Ort</label>
  <p></p>
</div>
      <blockquote class="embedly-card"><h4><a href="https://www.meetup.com/Youth-Entrepreneur-Warrior-Hong-Kong-%E9%9D%92%E5%B9%B4%E5%89%B5%E6%A5%AD%E8%BB%8D-%E9%A6%99%E6%B8%AF/">Youth Entrepreneur Warrior (Hong Kong) 青年創業軍 (香港) (Hong Kong, Hong Kong)</a></h4><p>Youth Entrepreneur Warrior is a famous youth entrepreneur organization in Hong Kong, bridging all youth entrepreneurs in Hong Kong, helping each other in this business world, and looking for any bright and new business opportunities. With regular and sometimes large-scale gathering events, we and our members are like a family, which facilitates Hong Kong youth entrepreneurs to share their feelings, their experiences and their opinions.</p></blockquote>
<script async src="//cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>
      TBD
      
      function fetchGroups(url, cb, data) {
	if(!data) data = [];
	
	$.ajax({
		
		dataType:'jsonp',
		method:'get',
		url:url,
		success:function(result) {
			console.log('back with ' + result.data.length +' results');
			console.dir(result);
			//add to data
			data.push.apply(data, result.data);
			if(result.meta.next_link) {
				var nextUrl = result.meta.next_link;
				fetchGroups(nextUrl, cb, data);
			} else {
				cb(data);	
			}
		}
	});	
	
}

$(document).ready(function() {
	
	var $results = $("#results");

	$results.html("<p>Finding meetups with Ionic in the description.</p>");

	fetchGroups("https://api.meetup.com/find/groups?&photo-host=public&page=50&text=ionic&sig_id=2109318&radius=global&order=newest&sig=ad335a79ccce2b1bb65b27fe10ea6836305e5533&callback=?", function(res) {
		console.log("totally done");
		console.dir(res);	

		var s = "";
		for(var i=0;i<res.length; i++) {
			var group = res[i];
			s += "<h2>"+(i+1)+" <a href='"+group.link+"'>"+group.name+"</a></h2>";
			if(group.group_photo && group.group_photo.thumb_link) {
				s += "<img src=\"" + group.group_photo.thumb_link + "\" align=\"left\">";
			}
			s += "<p>Location: "+group.city + ", " + group.state + " " + group.country + "</p><br clear=\"left\">";
		}
		$results.html(s);
		
		
	});
		
});
    </body>
    </html>
  
