In situations where you have existing web sites on your server, you may find it useful to run Jenkins (or the servlet container that Jenkins runs in) behind [Nginx](https://nginx.org/), so that you can bind Jenkins to the part of a bigger website that you may have. This section discusses some of the approaches for doing this.

When a request arrives for certain URLs, Nginx becomes a proxy and further forward that request to Jenkins, then it forwards the response back to the client. A typical set up for mod\_proxy would look like this:

```
upstream jenkins {
  keepalive 32; # keepalive connections
  server 127.0.0.1:8080; # jenkins ip and port
}

# Required for Jenkins websocket agents
map $http_upgrade $connection_upgrade {
  default upgrade;
  '' close;
}

server {
  listen          80;       # Listen on port 80 for IPv4 requests

  server_name     jenkins.example.com;  # replace 'jenkins.example.com' with your server domain name

  # this is the jenkins web root directory
  # (mentioned in the output of "systemctl cat jenkins")
  root            /var/run/jenkins/war/;

  access_log      /var/log/nginx/jenkins.access.log;
  error_log       /var/log/nginx/jenkins.error.log;

  # pass through headers from Jenkins that Nginx considers invalid
  ignore_invalid_headers off;

  location ~ "^/static/[0-9a-fA-F]{8}\/(.*)$" {
    # rewrite all static files into requests to the root
    # E.g /static/12345678/css/something.css will become /css/something.css
    rewrite "^/static/[0-9a-fA-F]{8}\/(.*)" /$1 last;
  }

  location /userContent {
    # have nginx handle all the static requests to userContent folder
    # note : This is the $JENKINS_HOME dir
    root /var/lib/jenkins/;
    if (!-f $request_filename){
      # this file does not exist, might be a directory or a /**view** url
      rewrite (.*) /$1 last;
      break;
    }
    sendfile on;
  }

  location / {
      sendfile off;
      proxy_pass         http://jenkins;
      proxy_redirect     default;
      proxy_http_version 1.1;

      # Required for Jenkins websocket agents
      proxy_set_header   Connection        $connection_upgrade;
      proxy_set_header   Upgrade           $http_upgrade;

      proxy_set_header   Host              $host;
      proxy_set_header   X-Real-IP         $remote_addr;
      proxy_set_header   X-Forwarded-For   $proxy_add_x_forwarded_for;
      proxy_set_header   X-Forwarded-Proto $scheme;
      proxy_max_temp_file_size 0;

      #this is the maximum upload size
      client_max_body_size       10m;
      client_body_buffer_size    128k;

      proxy_connect_timeout      90;
      proxy_send_timeout         90;
      proxy_read_timeout         90;
      proxy_buffering            off;
      proxy_request_buffering    off; # Required for HTTP CLI commands
      proxy_set_header Connection ""; # Clear for keepalive
  }

}
```

This assumes that you run Jenkins on port 8080. Remember to create the folder /var/log/nginx/jenkins.

For this set up to work, the context path of Jenkins must be the same between your Nginx and Jenkins (that is, you can’t run Jenkins on [http://localhost:8081/ci](http://localhost:8081/ci) and have it exposed at [http://localhost:80/jenkins](http://localhost/jenkins)).

Set the context path by modifying the jenkins.xml configuration file and adding --prefix=/jenkins to the <arguments> entry.

If you are having problems with some paths (eg folders) with **Blue Ocean**, you may need to add the following snippet to your proxy configuration:

```
if ($request_uri ~* "/blue(/.*)") {
    proxy_pass http://YOUR_SERVER_IP:YOUR_JENKINS_PORT/blue$1;
    break;
}
```

To give Nginx permission to read Jenkins web root folder, add the `nginx` user to the Jenkins group:

```
usermod -aG jenkins nginx
```

If the last command failed because the `nginx` user is not defined in the system, then you can try adding the `www-data` user to the Jenkins group:

```
usermod -aG jenkins www-data
```

If you are experiencing timeouts when attempting to run long CLI commands through a proxy in Jenkins, you can increase the `proxy_read_timeout` setting as necessary. Older versions of Jenkins may not respect the `proxy_read_timeout` setting.

If you are experiencing the following error when attempting to run long CLI commands in Jenkins and Jenkins is running behind Nginx, it is probably due to Nginx timing out the CLI connection. You can increase the `proxy_read_timeout` setting as necessary so the command will complete successfully.

```
WARNING: null
hudson.cli.DiagnosedStreamCorruptionException
Read back: 0x00 0x00 0x00 0x1e 0x07
           'Started reverse-proxy-test #68'
           0x00 0x00 0x00 0x01 0x07 0x0a
Read ahead:
Diagnosis problem:
    java.io.IOException: Premature EOF
        at sun.net.www.http.ChunkedInputStream.readAheadBlocking(ChunkedInputStream.java:565)
        ...
    at hudson.cli.FlightRecorderInputStream.analyzeCrash(FlightRecorderInputStream.java:82)
    at hudson.cli.PlainCLIProtocol$EitherSide$Reader.run(PlainCLIProtocol.java:153)
Caused by: java.io.IOException: Premature EOF
    at sun.net.www.http.ChunkedInputStream.readAheadBlocking(ChunkedInputStream.java:565)
    ...
    at java.io.DataInputStream.readInt(DataInputStream.java:387)
    at hudson.cli.PlainCLIProtocol$EitherSide$Reader.run(PlainCLIProtocol.java:111)
```

Please submit your feedback about this page through this [quick form](https://www.jenkins.io/doc/feedback-form/).

Alternatively, if you don't wish to complete the quick form, you can simply indicate if you found this page helpful?

See existing feedback [here](https://docs.google.com/spreadsheets/d/1IIdpVs39JDYKg0sLQIv-MNO928qcGApAIfdW5ohfD78).