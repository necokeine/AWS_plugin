set (CMAKE_CXX_STANDARD 11)

#if(BUILD_KINESIS_PLUGIN)
  file(GLOB HEADERS "include/eosio/mongo_db_plugin/*.hpp")
  include_directories("/usr/local/include")
  LINK_LIBRARIES("/usr/local/lib/librdkafka.so" "/usr/local/lib/librdkafka.so.1")
  link_directories("/usr/local/lib")
  add_library( kinesis_plugin
               kinesis_plugin.cpp kinesis_producer.cpp
               ${HEADERS} )
  target_include_directories(kinesis_plugin
          PUBLIC "include"
          )
  target_link_libraries(kinesis_plugin
          PUBLIC chain_plugin eosio_chain appbase fc
          )

  message("mongo_db_plugin not selected and will be omitted.")
#endif()
