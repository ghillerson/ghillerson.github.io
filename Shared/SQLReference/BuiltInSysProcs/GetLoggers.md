[Open topic with navigation](../../../index.html#Shared/SQLReference/BuiltInSysProcs/GetLoggers.html)

<a href="" id="BuiltInSysProcs.GetLoggers"></a>[]()SYSCS\_UTIL.SYSCS\_GET\_LOGGERS
==================================================================================

The SYSCS\_UTIL.SYSCS\_GET\_LOGGERS system procedure displays the names of all Splice Machine loggers in the system. Use this to find loggers of interest, if you want to determine or change their log levels.

<span class="autonumber"><span class="noteAutoNum">NOTE:  </span></span>You can read more about Splice  Machine loggers in the [Logging](../../Developers/TuningAndDebugging/UsingLogging.html) topic in our <span class="ItalicFont">Administrator's Guide</span>.

Syntax

``` FcnSyntax
SYSCS_UTIL.SYSCS_GET_LOGGERS()
```

Results

The displayed results of calling <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_LOGGERS</span> include these values:

| Value                                    | Description            |
|------------------------------------------|------------------------|
| <span class="CodeFont">LOGGERNAME</span> | The name of the logger |

Example

Here's the output from a call to <span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_LOGGERS</span>, as of Splice Machine Release 1.5:

``` Example
splice> CALL SYSCS_UTIL.SYSCS_GET_LOGGERS();
SPLICELOGGER                                                                  
------------------------------------------------------------------------------
com.splicemachine                                                             
com.splicemachine.async.HBaseClient                                           
com.splicemachine.async.QueueingAsyncScanner                                  
com.splicemachine.async.RegionClient                                          
com.splicemachine.async.RegionInfo                                            
com.splicemachine.async.Scanner                                               
com.splicemachine.concurrent.LoggingScheduledThreadPoolExecutor               
com.splicemachine.constants.SpliceConstants                                   
com.splicemachine.constants.environment.EnvUtils                              
com.splicemachine.db                                                          
com.splicemachine.db.impl.ast.AssignRSNVisitor                                
com.splicemachine.db.impl.ast.FindHashJoinColumns                             
com.splicemachine.db.impl.ast.FixSubqueryColRefs                              
com.splicemachine.db.impl.ast.JoinConditionVisitor                            
com.splicemachine.db.impl.ast.JsonTreeBuilderVisitor                          
com.splicemachine.db.impl.ast.PlanPrinter                                     
com.splicemachine.db.impl.ast.RowLocationColumnVisitor                        
com.splicemachine.db.impl.ast.SpliceDerbyVisitorAdapter                       
com.splicemachine.db.impl.jdbc.authentication                                 
com.splicemachine.db.impl.sql.catalog                                         
com.splicemachine.db.impl.sql.catalog.DefaultSystemProcedureGenerator         
com.splicemachine.db.impl.sql.compile.subquery.exists.ExistsSubqueryPredicate 
com.splicemachine.db.impl.sql.execute.operations                              
com.splicemachine.db.shared.common.sanity                                     
com.splicemachine.derby.ddl.AsynchronousDDLController                         
com.splicemachine.derby.ddl.DDLWatchRefresher                                 
com.splicemachine.derby.ddl.DDLZookeeperClient                                
com.splicemachine.derby.ddl.ZooKeeperDDLWatchChecker                          
com.splicemachine.derby.ddl.ZookeeperDDLWatcher                               
com.splicemachine.derby.hbase.AbstractSpliceIndexObserver                     
com.splicemachine.derby.hbase.AbstractSpliceIndexObserver.Compaction          
com.splicemachine.derby.hbase.AbstractSpliceIndexObserver.Split               
com.splicemachine.derby.hbase.ActivationSerializer                            
com.splicemachine.derby.hbase.RollForwardAction                               
com.splicemachine.derby.hbase.RollForwardTask                                 
com.splicemachine.derby.hbase.ShutdownRegionServerObserver                    
com.splicemachine.derby.hbase.SpliceBaseIndexEndpoint                         
com.splicemachine.derby.hbase.SpliceBaseOperationRegionScanner                
com.splicemachine.derby.hbase.SpliceDerbyCoprocessor                          
com.splicemachine.derby.hbase.SpliceDriver                                    
com.splicemachine.derby.hbase.SpliceIndexEndpoint                             
com.splicemachine.derby.hbase.SpliceIndexObserver                             
com.splicemachine.derby.hbase.SpliceMasterObserver                            
com.splicemachine.derby.hbase.SpliceObserverInstructions                      
com.splicemachine.derby.hbase.SpliceOperationRegionObserver                   
com.splicemachine.derby.hbase.SpliceOperationRegionScanner                    
com.splicemachine.derby.hbase.SpliceWriteControl                              
com.splicemachine.derby.iapi.sql.execute.OperationResultSet                   
com.splicemachine.derby.iapi.sql.execute.SpliceNoPutResultSet                 
com.splicemachine.derby.iapi.sql.execute.SpliceOperationContext               
com.splicemachine.derby.impl.SpliceMethod                                     
com.splicemachine.derby.impl.SpliceService                                    
com.splicemachine.derby.impl.db.SpliceDatabase                                
com.splicemachine.derby.impl.job.coprocessor.CoprocessorTaskScheduler         
com.splicemachine.derby.impl.job.operation.SinkTask                           
com.splicemachine.derby.impl.job.scheduler.BaseJobControl                     
com.splicemachine.derby.impl.job.scheduler.DistributedJobScheduler            
com.splicemachine.derby.impl.job.scheduler.JobControl                         
com.splicemachine.derby.impl.job.scheduler.RegionTaskControl                  
com.splicemachine.derby.impl.job.scheduler.TaskCallable                       
com.splicemachine.derby.impl.job.scheduler.WorkStealingTaskScheduler          
com.splicemachine.derby.impl.services.streams.ConfiguredStream                
com.splicemachine.derby.impl.spark.SpliceSpark                                
com.splicemachine.derby.impl.sql.catalog                                      
com.splicemachine.derby.impl.sql.catalog.SpliceDataDictionary                 
com.splicemachine.derby.impl.sql.catalog.upgrade                              
com.splicemachine.derby.impl.sql.compile.NestedLoopJoinStrategy               
com.splicemachine.derby.impl.sql.depend.SpliceDependencyManager               
com.splicemachine.derby.impl.sql.execute.LazyDataValueDescriptor              
com.splicemachine.derby.impl.sql.execute.LazyStringDataValueDescriptor        
com.splicemachine.derby.impl.sql.execute.LazyTimestampDataValueDescriptor     
com.splicemachine.derby.impl.sql.execute.SpliceExecutionFactory               
com.splicemachine.derby.impl.sql.execute.SpliceGenericConstantActionFactory   
com.splicemachine.derby.impl.sql.execute.SpliceGenericResultSetFactory        
com.splicemachine.derby.impl.sql.execute.SpliceRealResultSetStatisticsFactory 
com.splicemachine.derby.impl.sql.execute.actions.DeleteConstantOperation      
com.splicemachine.derby.impl.sql.execute.actions.TransactionReadTask          
com.splicemachine.derby.impl.sql.execute.operations.AnyOperation              
com.splicemachine.derby.impl.sql.execute.operations.BroadCastJoinRows         
com.splicemachine.derby.impl.sql.execute.operations.BroadcastJoinOperation    
com.splicemachine.derby.impl.sql.execute.operations.CachedOperation           
com.splicemachine.derby.impl.sql.execute.operations.CallStatementOperation    
com.splicemachine.derby.impl.sql.execute.operations.DMLWriteOperation         
com.splicemachine.derby.impl.sql.execute.operations.DeleteOperation           
com.splicemachine.derby.impl.sql.execute.operations.IndexRowReader            
com.splicemachine.derby.impl.sql.execute.operations.IndexRowToBaseRowOperation
com.splicemachine.derby.impl.sql.execute.operations.JoinOperation             
com.splicemachine.derby.impl.sql.execute.operations.JoinUtils                 
com.splicemachine.derby.impl.sql.execute.operations.Joiner                    
com.splicemachine.derby.impl.sql.execute.operations.MergeSortJoinOperation    
com.splicemachine.derby.impl.sql.execute.operations.NoRowsOperation           
com.splicemachine.derby.impl.sql.execute.operations.NormalizeOperation        
com.splicemachine.derby.impl.sql.execute.operations.OperationTree             
com.splicemachine.derby.impl.sql.execute.operations.ProjectRestrictOperation  
com.splicemachine.derby.impl.sql.execute.operations.RowOperation              
com.splicemachine.derby.impl.sql.execute.operations.ScanOperation             
com.splicemachine.derby.impl.sql.execute.operations.SpliceBaseOperation       
com.splicemachine.derby.impl.sql.execute.operations.SpliceBaseOperation.close 
com.splicemachine.derby.impl.sql.execute.operations.TableScanOperation        
com.splicemachine.derby.impl.sql.execute.operations.UpdateOperation           
com.splicemachine.derby.impl.sql.execute.operations.scanner.SITableScanner    
com.splicemachine.derby.impl.stats.CachedPhysicalStatsStore                   
com.splicemachine.derby.impl.stats.HBaseColumnStatisticsStore                 
com.splicemachine.derby.impl.stats.PartitionStatsStore                        
com.splicemachine.derby.impl.stats.StatisticsTask                             
com.splicemachine.derby.impl.stats.StatsConstants                             
com.splicemachine.derby.impl.storage.AbstractMultiScanProvider                
com.splicemachine.derby.impl.storage.AbstractScanProvider                     
com.splicemachine.derby.impl.storage.BaseHashAwareScanBoundary                
com.splicemachine.derby.impl.storage.ClientResultScanner                      
com.splicemachine.derby.impl.storage.ClientScanProvider                       
com.splicemachine.derby.impl.storage.DistributedClientScanProvider            
com.splicemachine.derby.impl.storage.MeasuredResultScanner                    
com.splicemachine.derby.impl.storage.MultiScanRowProvider                     
com.splicemachine.derby.impl.storage.RegionAwareScanner                       
com.splicemachine.derby.impl.storage.ReopenableScanner                        
com.splicemachine.derby.impl.storage.RowProviders                             
com.splicemachine.derby.impl.storage.SingleScanRowProvider                    
com.splicemachine.derby.impl.store.access.BaseSpliceTransaction               
com.splicemachine.derby.impl.store.access.HBaseStore                          
com.splicemachine.derby.impl.store.access.PropertyConglomerate                
com.splicemachine.derby.impl.store.access.SpliceAccessManager                 
com.splicemachine.derby.impl.store.access.SpliceLockFactory                   
com.splicemachine.derby.impl.store.access.SpliceTransaction                   
com.splicemachine.derby.impl.store.access.SpliceTransactionContext            
com.splicemachine.derby.impl.store.access.SpliceTransactionFactory            
com.splicemachine.derby.impl.store.access.SpliceTransactionManager            
com.splicemachine.derby.impl.store.access.SpliceTransactionManagerContext     
com.splicemachine.derby.impl.store.access.StatsStoreCostController            
com.splicemachine.derby.impl.store.access.base.SpliceConglomerate             
com.splicemachine.derby.impl.store.access.base.SpliceController               
com.splicemachine.derby.impl.store.access.base.SpliceScan                     
com.splicemachine.derby.impl.store.access.btree.IndexConglomerate             
com.splicemachine.derby.impl.store.access.btree.IndexConglomerateFactory      
com.splicemachine.derby.impl.store.access.btree.IndexController               
com.splicemachine.derby.impl.store.access.hbase.HBaseConglomerate             
com.splicemachine.derby.impl.store.access.hbase.HBaseController               
com.splicemachine.derby.impl.temp.TempTable                                   
com.splicemachine.derby.jdbc.SpliceTransactionResourceImpl                    
com.splicemachine.derby.logging.DerbyOutputLoggerWriter                       
com.splicemachine.derby.management.StatementManager                           
com.splicemachine.derby.management.TransactionalSysTableWriter                
com.splicemachine.derby.utils.ConglomerateUtils                               
com.splicemachine.derby.utils.DerbyBytesUtil                                  
com.splicemachine.derby.utils.Scans                                           
com.splicemachine.derby.utils.SpliceAdmin                                     
com.splicemachine.derby.utils.SpliceUtils                                     
com.splicemachine.derby.utils.StatisticsAdmin                                 
com.splicemachine.hbase.AbstractBufferedRegionScanner                         
com.splicemachine.hbase.BufferedRegionScanner                                 
com.splicemachine.hbase.HBaseRegionLoads                                      
com.splicemachine.hbase.NoRetryCoprocessorRpcChannel                          
com.splicemachine.hbase.backup.Backup                                         
com.splicemachine.hbase.backup.BackupHFileCleaner                             
com.splicemachine.hbase.backup.BackupReporter                                 
com.splicemachine.hbase.backup.BackupSystemProcedures                         
com.splicemachine.hbase.backup.BackupUtils                                    
com.splicemachine.hbase.backup.SnapshotUtilsBase                              
com.splicemachine.hbase.backup.SnapshotUtilsImpl                              
com.splicemachine.hbase.regioninfocache.HBaseRegionCache                      
com.splicemachine.hbase.table.BetterHTablePool                                
com.splicemachine.hbase.table.SpliceHTable                                    
com.splicemachine.hbase.table.SpliceHTableFactory                             
com.splicemachine.job.CompositeJobResults                                     
com.splicemachine.job.ZkTaskMonitor                                           
com.splicemachine.mrio.api                                                    
com.splicemachine.pipeline.callbuffer.PipingCallBuffer                        
com.splicemachine.pipeline.callbuffer.RegionServerCallBuffer                  
com.splicemachine.pipeline.ddl.DDLChange                                      
com.splicemachine.pipeline.exception.SpliceDoNotRetryIOException              
com.splicemachine.pipeline.impl.BulkWriteAction                               
com.splicemachine.pipeline.impl.BulkWriteAction.retries                       
com.splicemachine.pipeline.impl.BulkWriteChannelInvoker                       
com.splicemachine.pipeline.threadpool.MonitoredThreadPool                     
com.splicemachine.pipeline.utils.PipelineConstants                            
com.splicemachine.pipeline.utils.PipelineUtils                                
com.splicemachine.pipeline.writeconfiguration.BaseWriteConfiguration          
com.splicemachine.pipeline.writecontext.PipelineWriteContext                  
com.splicemachine.pipeline.writecontextfactory.LocalWriteContextFactory       
com.splicemachine.pipeline.writehandler.RegionWriteHandler                    
com.splicemachine.queryPlan                                                   
com.splicemachine.si.api.Txn                                                  
com.splicemachine.si.coprocessors.SIBaseObserver                              
com.splicemachine.si.coprocessors.SIObserver                                  
com.splicemachine.si.coprocessors.TimestampMasterObserver                     
com.splicemachine.si.coprocessors.TxnLifecycleEndpoint                        
com.splicemachine.si.impl.BaseSIFilter                                        
com.splicemachine.si.impl.ClientTxnLifecycleManager                           
com.splicemachine.si.impl.PackedTxnFilter                                     
com.splicemachine.si.impl.ReadOnlyTxn                                         
com.splicemachine.si.impl.SITransactor                                        
com.splicemachine.si.impl.WritableTxn                                         
com.splicemachine.si.impl.readresolve.AsyncReadResolver                       
com.splicemachine.si.impl.readresolve.SynchronousReadResolver                 
com.splicemachine.si.impl.region.RegionTxnStore                               
com.splicemachine.si.impl.region.TransactionResolver                          
com.splicemachine.si.impl.rollforward.SegmentedRollForward                    
com.splicemachine.si.impl.timestamp.TimestampClient                           
com.splicemachine.si.impl.timestamp.TimestampOracle                           
com.splicemachine.tools.version.ManifestFinder                                
com.splicemachine.utils.SpliceUtilities                                       
com.splicemachine.utils.SpliceZooKeeperManager                                
com.splicemachine.utils.ZkUtils                                               

203 rows selected
```

See Also

-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_GET\_LOGGER\_LEVEL</span>](GetLoggerLevel.html)
-   [<span class="CodeFont">SYSCS\_UTIL.SYSCS\_SET\_LOGGER\_LEVEL</span>](SetLoggerLevel.html)

 


