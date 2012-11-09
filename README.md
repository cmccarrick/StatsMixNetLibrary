StatsMixNetLibrary
==================

A C# dll library for the StatsMix Service

This works with teh StatsMix site: http://www.statsmix.com/

I needed a library that provided a dll because for some projects we are still using VS 2008, which does not support NuGet

I also made some changes to the code to support async calls and added some new overloads

See the StatsMixNetLibrary2 if you need to support .Net 2.0.

Example usage for async use.  Use this for situation when you cannot wait for the REST API result due to performance issues with your application.  Make sure to wrap in a Try Catch block.

            Client smClient = new Client("API_KEY");
            //add optional meta information
            var meta = new Dictionary<string, string>();
            meta.Add("Customer", _CustomerName);
            meta.Add("Domain", _SenderDomain);
            Task.Factory.StartNew(() => smClient.trackasync("METRIC_NAME", 1, meta));


Example usage for sync use.  Use this for situation when it is ok to block waiting for the metric update and for initial testing.

            Client smClient = new Client("API_KEY");
            //add optional meta information
            var meta = new Dictionary<string, string>();
            meta.Add("Customer", _CustomerName);
            meta.Add("Domain", _SenderDomain);
            String resp = smClient.track("METRIC_NAME", 1, meta));


