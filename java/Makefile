
all:
	(cd .. && go build -buildmode=c-shared && mv libtailscale java/libtailscale.dylib)
	cc -I$(JAVA_HOME)/include -I$(JAVA_HOME)/include/darwin -o libtailscalejni.dylib -shared tailscalejni.c libtailscale.dylib
	$(JAVA_HOME)/bin/javac Tailscale.java
	mkdir -p com/tailscale
	mv *.class com/tailscale/

test: all
	(cd ../libtestcontrol && go build -buildmode=c-shared && mv libtestcontrol ../java/libtestcontrol.dylib)
	cc -I$(JAVA_HOME)/include -I$(JAVA_HOME)/include/darwin -o libtestcontroljni.dylib -shared tailscalejni_test.c libtestcontrol.dylib
	$(JAVA_HOME)/bin/javac TailscaleTest.java
	mv *.class com/tailscale/
	$(JAVA_HOME)/bin/java -cp . -Djdk.http.auth.tunneling.disabledSchemes="" -Djdk.http.auth.proxying.disabledSchemes="" com.tailscale.TailscaleTest
