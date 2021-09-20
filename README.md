# jmeter-graph-tool-maven-plugin

A maven plugin to create graphs using the **JMeter Plugins CMDRunner** from JMeter result files (\*.jtl or \*.csv) or using **Filter Results Tool**.

See [https://jmeter-plugins.org/wiki/JMeterPluginsCMD/](https://jmeter-plugins.org/wiki/JMeterPluginsCMD/) for more informations for graphs and graphs parameters.

See [https://jmeter-plugins.org/wiki/FilterResultsTool/](https://jmeter-plugins.org/wiki/FilterResultsTool/) form more informations for Filter Result Tools

A fork from project [jmeter-graph-maven-plugin project](https://github.com/codecentric/jmeter-graph-maven-plugin) and renamed project, add 'tool' to the artifactId. With the permission of the old main developper Michael Lex (september 2021).

Note: DBMon monitoring graph do not work with this version (log library trouble)


## License
See the LICENSE file (Apache 2) [https://www.apache.org/licenses/LICENSE-2.0](https://www.apache.org/licenses/LICENSE-2.0)

## Usage


Just include the plugin in your `pom.xml` and execute `mvn jmeter-graph:create-graph`.

```xml
<project>
    <!-- ... -->
    <build>
        <plugins>
            <plugin>
                <groupId>io.github.vdaburon</groupId>
                <artifactId>jmeter-graph-tool-maven-plugin</artifactId>
                <version>1.0</version>
                <configuration>
                    <!-- see Filter Results Tool in jmeter-plugins.org -->
                    <filterResultsTool>
                        <filterResultsParam>
                            <inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
                            <outputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_regex_filtred.csv</outputFile>
                            <successFilter>false</successFilter>
                            <includeLabels>0.*</includeLabels>
                            <includeLabelRegex>true</includeLabelRegex>
                        </filterResultsParam>
                        <filterResultsParam>
                            <inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
                            <outputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_offset_filtred.jtl</outputFile>
                            <successFilter>false</successFilter>
                            <startOffset>2</startOffset>
                            <endOffset>20</endOffset>
                            <saveAsXml>true</saveAsXml>
                        </filterResultsParam>
                    </filterResultsTool>
                    <graphs>
                      <!-- see JMeterPluginsCMD Command Line Tool in jmeter-plugins.org -->
                        <graph>
                            <pluginType>ResponseTimesOverTime</pluginType>
                            <inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
                            <generatePng>${project.build.directory}/jmeter/results/ResponseTimesOverTime.png</generatePng>
                            <width>800</width>
                            <height>600</height>
                            <limitRows>50</limitRows>
                            <relativeTimes>no</relativeTimes>
                            <paintGradient>no</paintGradient>
                            <startOffset>2</startOffset>
                            <endOffset>20</endOffset>
                            <includeLabels>0.*</includeLabels>
                            <includeLabelRegex>true</includeLabelRegex>
                            <forceY>1000</forceY>
                            <autoScale>no</autoScale>
                            <lineWeight>2</lineWeight>
                        </graph>
                        <graph>
                            <inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
                            <pluginType>TransactionsPerSecond</pluginType>
                            <width>800</width>
                            <height>600</height>
                            <generatePng>${project.build.directory}/jmeter/results/TransactionsPerSecond.png</generatePng>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>yes</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                        <!-- Page Data Extractor -->
                        <graph>
                            <pluginType>PageDataExtractorOverTime</pluginType>
                            <inputFile>${project.build.directory}/jmeter/results/pde_httpd.jtl</inputFile>
                            <generatePng>${project.build.directory}/jmeter/results/pde_httpd_all_workers.png</generatePng>
                            <extractorRegexps>(BusyWorkers|IdleWorkers):.*{;}[A-Za-z]+:.([0-9]+){;}false{;}true</extractorRegexps>
                            <width>1024</width>
                            <height>800</height>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>no</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                        <graph>
                            <pluginType>PageDataExtractorOverTime</pluginType>
                            <inputFile>${project.build.directory}/jmeter/results/pde_httpd.jtl</inputFile>
                            <generatePng>${project.build.directory}/jmeter/results/pde_httpd_busy_workers.png</generatePng>
                            <extractorRegexps>(BusyWorkers):.*{;}BusyWorkers:.([0-9]+){;}false{;}true</extractorRegexps>
                            <width>1024</width>
                            <height>800</height>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>no</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                        <!-- PerfMon -->
                        <graph>
                            <pluginType>PerfMon</pluginType>
                            <inputFile>${project.build.directory}/jmeter/results/perfmon.csv</inputFile>
                            <generatePng>${project.build.directory}/jmeter/results/Perfmon_CPU.png</generatePng>
                            <includeLabels>.*CPU.*</includeLabels>
                            <includeLabelRegex>true</includeLabelRegex>
                            <width>1024</width>
                            <height>800</height>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>no</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                        <graph>
                            <pluginType>PerfMon</pluginType>
                            <inputFile>${project.build.directory}/jmeter/results/perfmon.csv</inputFile>
                            <generatePng>${project.build.directory}/jmeter/results/Perfmon_Memory.png</generatePng>
                            <includeLabels>.*Memory.*</includeLabels>
                            <includeLabelRegex>true</includeLabelRegex>
                            <width>1024</width>
                            <height>800</height>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>no</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                        <!-- JMXMon -->
                        <graph>
                            <pluginType>JMXMon</pluginType>
                            <inputFile>${project.build.directory}/jmeter/results/gest_jmx_tomcat.jtl</inputFile>
                            <generatePng>${project.build.directory}/jmeter/results/JMX_memory_jvm.png</generatePng>
                            <includeLabels>used.HeapMemoryUsage.*</includeLabels>
                            <includeLabelRegex>true</includeLabelRegex>
                            <width>1024</width>
                            <height>800</height>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>no</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                        <graph>
                            <pluginType>JMXMon</pluginType>
                            <inputFile>${project.build.directory}/jmeter/results/gest_jmx_tomcat.jtl</inputFile>
                            <generatePng>${project.build.directory}/jmeter/results/JMX_currentThreadsBusy.png</generatePng>
                            <includeLabels>.*currentThreadsBusy.*</includeLabels>
                            <includeLabelRegex>true</includeLabelRegex>
                            <width>1024</width>
                            <height>800</height>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>no</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                        <!-- Aggregate report csv -->
                        <graph>
                            <inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
                            <pluginType>AggregateReport</pluginType>
                            <generateCsv>${project.build.directory}/jmeter/results/AggregateReport.csv</generateCsv>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>no</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                        <graph>
                            <inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
                            <pluginType>ResponseCodesPerSecond</pluginType>
                            <width>800</width>
                            <height>600</height>
                            <generatePng>${project.build.directory}/jmeter/results/ResponseCodesPerSecond.png</generatePng>
                            <relativeTimes>no</relativeTimes>
                            <aggregateRows>no</aggregateRows>
                            <paintGradient>no</paintGradient>
                        </graph>
                    </graphs>
                    <!- copy files from directoryTestFiles to JMETER_HOME/bin -->
                    <directoryTestFiles>${project.build.directory}/jmeter/testFiles</directoryTestFiles>
                    <!-- see jmeter-maven-pugins -->
                    <jMeterProcessJVMSettings>
                        <xms>${jvm_xms}</xms>
                        <xmx>${jvm_xmx}</xmx>
                    </jMeterProcessJVMSettings>
                    <!-- merge this properties with user.properties file in JMETER_HOME/bin -->
                    <!-- property format = <property_name>property_value</property name> will be property_name=property_value in the user.properties file. E.g. language=en -->
                    <propertiesUser>
                        <language>en</language>
                    </propertiesUser>
            </configuration>
        </plugin>
    </plugins>
  </build>
</project>
```

You can also bind the graph-generation to a maven-phase, e.g. `verify`:

```xml
<project>
  <!-- ... -->
  <build>
    <plugins>
      <plugin>
        <groupId>io.github.vdaburon</groupId>
        <artifactId>jmeter-graph-tool-maven-plugin</artifactId>
        <version>1.0</version>
        <executions>
          <execution>
            <id>create-graphs</id>
            <goals>
              <goal>create-graph</goal>
            </goals>
            <phase>verify</phase>
            <configuration>
              <!-- ... you can declare filterResultsTool here -->
             <graphs>
                <graph>
                    <pluginType>ResponseTimesOverTime</pluginType>
                    <inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
                    <generatePng>${project.build.directory}/jmeter/results/ResponseTimesOverTime.png</generatePng>
                    <width>800</width>
                    <height>600</height>
                </graph>
                <!-- ... you can declare more <graph> here -->
              </graphs>
            </configuration>
          </execution>
        </execution>
      </plugin>
    </plugins>
  </build>
</project>
```

### Parameters for a graph (depends of the pluginType) :
- inputFile
- pluginType
- width
- height
- generatePng
- generateCsv
- granulation
- relativeTimes
- aggregateRows
- paintGradient
- paintZeroing
- paintMarkers
- preventOutliers
- limitRows
- forceY
- hideLowCounts
- successFilter
- includeLabels
- excludeLabels
- autoScale
- lineWeight
- extractorRegexps
- includeLabelRegex
- excludeLabelRegex
- startOffset
- endOffset

### List of the graph plugins type
- AggregateReport
- SynthesisReport
- ThreadsStateOverTime
- BytesThroughputOverTime
- HitsPerSecond
- LatenciesOverTime
- PerfMon
- DbMon (trouble with this plugin because log library error)
- JMXMon
- ResponseCodesPerSecond
- ResponseTimesDistribution
- ResponseTimesOverTime
- ResponseTimesPercentiles
- ThroughputVsThreads
- TimesVsThreads
- TransactionsPerSecond
- PageDataExtractorOverTime

### Parameters for a filterResultsTool
- inputFile
- outputFile
- successFilter
- includeLabels
- includeLabelRegex
- excludeLabels
- excludeLabelRegex
- startOffset
- endOffset
- saveAsXml



A full example, use **jmeter-maven-plugin** and **jmeter-graph-tool-maven-plugin**. Launch load test and the monitoring (PerfMon, JMXMon, Page Data Extractor), then filter results and generate graphs and Aggregate Report.

Use maven-phase `verify`

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>io.github.vdaburon.jmeter</groupId>
	<artifactId>jm_maven</artifactId>
	<version>1.1</version>
	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<maven.compiler.source>1.8</maven.compiler.source>
		<maven.compiler.target>1.8</maven.compiler.target>
		<jvm_xms>256</jvm_xms>
		<jvm_xmx>756</jvm_xmx>
		<nb_vusers>20</nb_vusers>
		<duration>180</duration>
	</properties>

	<build>
		<plugins>
				
			<plugin>
				<groupId>com.lazerycode.jmeter</groupId>
				<artifactId>jmeter-maven-plugin</artifactId>
				<version>3.4.0</version>
				<executions>
					<!-- Generate JMeter configuration -->
					<execution>
						<id>configuration</id>
						<goals>
							<goal>configure</goal>
						</goals>
					</execution>
					<!-- Run JMeter tests -->
					<execution>
						<id>jmeter-tests</id>
						<goals>
							<goal>jmeter</goal>
						</goals>
					</execution>
					<!-- Fail build on errors in test 
					<execution>
						<id>jmeter-check-results</id>
						<goals>
							<goal>results</goal>
						</goals>
					</execution>
					-->
				</executions>
				<configuration>
					<jmeterExtensions>
						<artifact>kg.apc:jmeter-plugins-functions:2.1</artifact>
						<artifact>kg.apc:jmeter-plugins-casutg:2.9</artifact>
						<artifact>kg.apc:jmeter-plugins-dummy:0.4</artifact>
						<artifact>kg.apc:jmeter-plugins-dbmon:0.1</artifact>
						<artifact>kg.apc:jmeter-plugins-jmxmon:0.3</artifact>
						<artifact>kg.apc:jmeter-plugins-pde:0.1</artifact>
						<artifact>kg.apc:jmeter-plugins-perfmon:2.1</artifact>
						<artifact>kg.apc:jmeter-plugins-graphs-basic:2.0</artifact>
						<artifact>kg.apc:jmeter-plugins-cmn-jmeter:0.3</artifact>
					</jmeterExtensions>
					<excludedArtifacts>
						<exclusion>commons-pool2:commons-pool2</exclusion>
					</excludedArtifacts>
					
					<!-- The plugin uses some broken dependencies An alternative is to set 
						this to true and use excludedArtifacts, see below -->
					<downloadExtensionDependencies>true</downloadExtensionDependencies>
					<jMeterProcessJVMSettings>
						<xms>${jvm_xms}</xms>
						<xmx>${jvm_xmx}</xmx>
					</jMeterProcessJVMSettings>
					<propertiesUser>
						<!-- project directory for this script, dedicated property use in the JMeter script to read csv file for example -->
						<dirProjet>${project.build.directory}/jmeter</dirProjet>
						<!-- nb_users and load test duration could be changed with mvn -Dparam=value, e.g. -Dnb_vusers=10 to replace default value (10 replace 20)-->
						<nb_vusers>${nb_vusers}</nb_vusers>
						<duration>${duration}</duration>
					</propertiesUser>
					<generateReports>false</generateReports>
					<testResultsTimestamp>false</testResultsTimestamp>
					<resultsFileFormat>csv</resultsFileFormat>
				</configuration>
			</plugin>
			<plugin>
				<groupId>io.github.vdaburon</groupId>
				<artifactId>jmeter-graph-tool-maven-plugin</artifactId>
				<version>1.0</version>
				<executions>
					<execution>
						<id>create-graphs</id>
						<goals>
							<goal>create-graph</goal>
						</goals>
						<phase>verify</phase>
						<configuration>
							<directoryTestFiles>${project.build.directory}/jmeter/testFiles</directoryTestFiles>
							<filterResultsTool>
								<filterResultsParam>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<outputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_regex_filtred.csv</outputFile>
									<successFilter>false</successFilter>
									<includeLabels>0.*</includeLabels>
									<includeLabelRegex>true</includeLabelRegex>
								</filterResultsParam>
								<filterResultsParam>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<outputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_offset_filtred.jtl</outputFile>
									<successFilter>false</successFilter>
									<startOffset>2</startOffset>
									<endOffset>20</endOffset>
									<saveAsXml>true</saveAsXml>
								</filterResultsParam>
							</filterResultsTool>
 						
							<graphs>
								<graph>
									<pluginType>AggregateReport</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<generateCsv>${project.build.directory}/jmeter/results/AggregateReport.csv</generateCsv>
								</graph>
								
								<graph>
									<pluginType>ResponseTimesOverTime</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<generatePng>${project.build.directory}/jmeter/results/ResponseTimesOverTime.png</generatePng>
									<width>800</width>
									<height>600</height>
									<limitRows>50</limitRows>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
									<startOffset>2</startOffset>
									<endOffset>20</endOffset>
									<includeLabels>0.*</includeLabels>
									<includeLabelRegex>true</includeLabelRegex>
									<forceY>1000</forceY>
									<autoScale>no</autoScale>
									<lineWeight>4</lineWeight>
								</graph>
								
								<graph>
									<pluginType>LatenciesOverTime</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<width>800</width>
									<height>600</height>
									<generatePng>${project.build.directory}/jmeter/results/LatenciesOverTime.png</generatePng>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>ResponseCodesPerSecond</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<width>800</width>
									<height>600</height>
									<generatePng>${project.build.directory}/jmeter/results/ResponseCodesPerSecond.png</generatePng>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>ResponseTimesDistribution</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<width>800</width>
									<height>600</height>
									<generatePng>${project.build.directory}/jmeter/results/ResponseTimesDistribution.png</generatePng>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>ResponseTimesOverTime</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<width>800</width>
									<height>600</height>
									<generatePng>${project.build.directory}/jmeter/results/ResponseTimesOverTime.png</generatePng>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>ResponseTimesPercentiles</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<width>800</width>
									<height>600</height>
									<generatePng>${project.build.directory}/jmeter/results/ResponseTimesPercentiles.png</generatePng>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>ThroughputVsThreads</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<width>800</width>
									<height>600</height>
									<generatePng>${project.build.directory}/jmeter/results/ThroughputVsThreads.png</generatePng>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>TimesVsThreads</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<width>800</width>
									<height>600</height>
									<generatePng>${project.build.directory}/jmeter/results/TimesVsThreads.png</generatePng>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>TransactionsPerSecond</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gestdoc_sc01_menu_local_monit.csv</inputFile>
									<width>800</width>
									<height>600</height>
									<generatePng>${project.build.directory}/jmeter/results/TransactionsPerSecond.png</generatePng>
									<relativeTimes>no</relativeTimes>
									<aggregateRows>yes</aggregateRows>
									<paintGradient>no</paintGradient>
								</graph>
								<!-- graphs from monitoring -->
								<graph>
							 		<pluginType>PageDataExtractorOverTime</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/pde_httpd.jtl</inputFile>
									<generatePng>${project.build.directory}/jmeter/results/pde_httpd_all_workers.png</generatePng>
									<extractorRegexps>(BusyWorkers|IdleWorkers):.*{;}[A-Za-z]+:.([0-9]+){;}false{;}true</extractorRegexps>
									<width>1024</width>
									<height>800</height>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>PageDataExtractorOverTime</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/pde_httpd.jtl</inputFile>
									<generatePng>${project.build.directory}/jmeter/results/pde_httpd_busy_workers.png</generatePng>
									<extractorRegexps>(BusyWorkers):.*{;}BusyWorkers:.([0-9]+){;}false{;}true</extractorRegexps>
									<width>1024</width>
									<height>800</height>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>PerfMon</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/perfmon.csv</inputFile>
									<generatePng>${project.build.directory}/jmeter/results/Perfmon_CPU.png</generatePng>
									<includeLabels>.*CPU.*</includeLabels>
									<includeLabelRegex>true</includeLabelRegex>
									<width>1024</width>
									<height>800</height>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>PerfMon</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/perfmon.csv</inputFile>
									<generatePng>${project.build.directory}/jmeter/results/Perfmon_Memory.png</generatePng>
									<includeLabels>.*Memory.*</includeLabels>
									<includeLabelRegex>true</includeLabelRegex>
									<width>1024</width>
									<height>800</height>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>JMXMon</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gest_jmx_tomcat.jtl</inputFile>
									<generatePng>${project.build.directory}/jmeter/results/JMX_memory_jvm.png</generatePng>
									<includeLabels>used.HeapMemoryUsage.*</includeLabels>
									<includeLabelRegex>true</includeLabelRegex>
									<width>1024</width>
									<height>800</height>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
								<graph>
									<pluginType>JMXMon</pluginType>
									<inputFile>${project.build.directory}/jmeter/results/gest_jmx_tomcat.jtl</inputFile>
									<generatePng>${project.build.directory}/jmeter/results/JMX_currentThreadsBusy.png</generatePng>
									<includeLabels>.*currentThreadsBusy.*</includeLabels>
									<includeLabelRegex>true</includeLabelRegex>
									<width>1024</width>
									<height>800</height>
									<relativeTimes>no</relativeTimes>
									<paintGradient>no</paintGradient>
								</graph>
							 </graphs>

							<jMeterProcessJVMSettings>
								<xms>${jvm_xms}</xms>
								<xmx>${jvm_xmx}</xmx>
							</jMeterProcessJVMSettings>
							<propertiesUser>
								<language>en</language>
							</propertiesUser>
						</configuration>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>

</project>
```
