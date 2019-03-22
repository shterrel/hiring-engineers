Your answers to the questions go here.

pythong scrypte for creating Timeboard.

from datadog import initialize, api

options = {
    'api_key': '0cd542dc44bea92cdd5cd0a6ceb535b7',
    'app_key': 'd8b672bec1750306941687fab943563f4443d0f0'
}

initialize(**options)

title = 'Challange Dashboard'
widgets = [
    {"definition": {
      "type": "timeseries",
      "requests": [
        {"q": "avg:my_metric{host:data-dog-test}"}
      ],
      "title": "My_Metric Info"
    }},
    {"definition": {
      "type": "timeseries",
      "requests": [
        {"q": "anomalies(avg:mysql.performance.cpu_time{*}, 'basic', 2)"}
      ],
      "title": "Anomaly graph for mysql performance cpu"
    }},
    {"definition": {
      "type": "timeseries",
      "requests": [
        {"q": "avg:my_metric{host:data-dog-test}.rollup(sum, 3600)"}
      ],
      "title": "My_Metric rollup sum Info"
    }}
   ]
layout_type = 'ordered'
description = '.'
is_read_only = True
notify_list = ['shterrel@gmail.com']
template_variables = [{
    'name': 'datadog-test',
    'prefix': 'host',
    'default': 'data-dog-test'
}]
api.Dashboard.create(title=title,
                     widgets=widgets,
                     layout_type=layout_type,
                     description=description,
                     is_read_only=is_read_only,
                     notify_list=notify_list,
                     template_variables=template_variables)

