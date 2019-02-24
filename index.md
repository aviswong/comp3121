<html>
  <head>
    <title>
      comp
    </title>
      <script type="text/javascript">
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
      
      TBD
    </body>
    </html>
  
