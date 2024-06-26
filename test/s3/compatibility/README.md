# Running S3 Compatibility tests against SeaweedFS

This is using [the tests from CephFS][s3-tests].

[s3-tests]: https://github.com/ceph/s3-tests

## Prerequisites

- have [Docker][docker] installed
- this has been executed on Mac. On Linux, the hostname in `s3tests.conf`  needs to be adjusted.

[docker]: https://docs.docker.com

## Running tests

To build the docker image that is used for the tests:

```console
./prepare.sh
```

To execute all tests:

```console
./run.sh
```
To see debug output including all commands run by the script:

```console
DEBUG=y ./run.sh
```

> [!WARNING]
>
> If your output does *not* look like the content in [`results.summary.txt`](./results.summary.txt)
> and it is full of HTTP level exceptions, there is likely an error contacting the `weed` server from
> the container that is runnin the S3 compatibility tests.
>
> There are at least a couple ways to solve this:
>
> - Modify your `docker` setup to ensure `host.docker.internal` is connected to your host running `weed`
> - Use `--net=host` and modify `host` in `s3tests.conf` to `localhost`
>
> The `--net=host` solution is potentially *unsafe*, as the container running [s3-tests][s3-tests] could
> visit unexpected websites or use the host-passthrough internet access maliciously.
>
> If you are OK with the risk of allowing `--net=host`:
>
> - Set `host = localhost` in `s3tests.conf`
> - Set `DOCKER_NET_HOST=y` when running `run.sh`

## Most recent results

See [`results.summary.txt`](./results.summary.txt) for the latest results of compatibility testing (with the caveat that `s3-tests` is pinned to [`ceph/s3-tests` @ 9a6a1e9f197fc9fb031b809d1e057635c2ff8d4e](https://github.com/ceph/s3-tests/commit/9a6a1e9f197fc9fb031b809d1e057635c2ff8d4e)).

The file is reproduced below for ease of access:

```
/s3-tests/virtualenv/lib/python3.6/site-packages/boto3/compat.py:88: PythonDeprecationWarning: Boto3 will no longer support Python 3.6 starting May 30, 2022. To continue receiving service updates, bug fixes, and security updates please upgrade to Python 3.7 or later. More information can be found here: https://aws.amazon.com/blogs/developer/python-support-policy-updates-for-aws-sdks-and-tools/
  warnings.warn(warning, PythonDeprecationWarning)
s3tests_boto3.functional.test_s3.test_bucket_list_return_data ... ERROR
s3tests_boto3.functional.test_s3.test_object_write_to_nonexist_bucket ... FAIL
s3tests_boto3.functional.test_s3.test_object_read_not_exist ... ok
s3tests_boto3.functional.test_s3.test_object_requestid_matches_header_on_error ... FAIL
s3tests_boto3.functional.test_s3.test_multi_object_delete ... ok
s3tests_boto3.functional.test_s3.test_multi_objectv2_delete ... ok
s3tests_boto3.functional.test_s3.test_multi_object_delete_key_limit ... ok
s3tests_boto3.functional.test_s3.test_multi_objectv2_delete_key_limit ... ok
s3tests_boto3.functional.test_s3.test_object_head_zero_bytes ... ok
s3tests_boto3.functional.test_s3.test_object_write_check_etag ... ok
s3tests_boto3.functional.test_s3.test_object_write_cache_control ... ok
s3tests_boto3.functional.test_s3.test_object_write_expires ... ok
s3tests_boto3.functional.test_s3.test_object_write_read_update_read_delete ... ok
s3tests_boto3.functional.test_s3.test_object_metadata_replaced_on_put ... ok
s3tests_boto3.functional.test_s3.test_object_write_file ... ok
s3tests_boto3.functional.test_s3.test_post_object_anonymous_request ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_authenticated_request ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_authenticated_no_content_type ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_authenticated_request_bad_access_key ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_set_success_code ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_set_invalid_success_code ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_upload_larger_than_chunk ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_set_key_from_filename ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_ignored_header ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_case_insensitive_condition_fields ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_escaped_field_values ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_success_redirect_action ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_invalid_signature ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_invalid_access_key ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_invalid_date_format ... ok
s3tests_boto3.functional.test_s3.test_post_object_no_key_specified ... ok
s3tests_boto3.functional.test_s3.test_post_object_missing_signature ... ok
s3tests_boto3.functional.test_s3.test_post_object_missing_policy_condition ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_user_specified_header ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_request_missing_policy_specified_field ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_condition_is_case_sensitive ... ok
s3tests_boto3.functional.test_s3.test_post_object_expires_is_case_sensitive ... ok
s3tests_boto3.functional.test_s3.test_post_object_expired_policy ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_invalid_request_field_value ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_missing_expires_condition ... ok
s3tests_boto3.functional.test_s3.test_post_object_missing_conditions_list ... ok
s3tests_boto3.functional.test_s3.test_post_object_upload_size_limit_exceeded ... ok
s3tests_boto3.functional.test_s3.test_post_object_missing_content_length_argument ... ok
s3tests_boto3.functional.test_s3.test_post_object_invalid_content_length_argument ... ok
s3tests_boto3.functional.test_s3.test_post_object_upload_size_below_minimum ... ok
s3tests_boto3.functional.test_s3.test_post_object_empty_conditions ... ok
s3tests_boto3.functional.test_s3.test_get_object_ifmatch_good ... ok
s3tests_boto3.functional.test_s3.test_get_object_ifmatch_failed ... ok
s3tests_boto3.functional.test_s3.test_get_object_ifnonematch_good ... ok
s3tests_boto3.functional.test_s3.test_get_object_ifnonematch_failed ... ok
s3tests_boto3.functional.test_s3.test_get_object_ifmodifiedsince_good ... ok
s3tests_boto3.functional.test_s3.test_get_object_ifmodifiedsince_failed ... ok
s3tests_boto3.functional.test_s3.test_get_object_ifunmodifiedsince_good ... ok
s3tests_boto3.functional.test_s3.test_get_object_ifunmodifiedsince_failed ... ok
s3tests_boto3.functional.test_s3.test_put_object_ifmatch_good ... ok
s3tests_boto3.functional.test_s3.test_put_object_ifmatch_failed ... FAIL
s3tests_boto3.functional.test_s3.test_put_object_ifmatch_overwrite_existed_good ... ok
s3tests_boto3.functional.test_s3.test_put_object_ifmatch_nonexisted_failed ... FAIL
s3tests_boto3.functional.test_s3.test_put_object_ifnonmatch_good ... ok
s3tests_boto3.functional.test_s3.test_put_object_ifnonmatch_failed ... FAIL
s3tests_boto3.functional.test_s3.test_put_object_ifnonmatch_nonexisted_good ... ok
s3tests_boto3.functional.test_s3.test_put_object_ifnonmatch_overwrite_existed_failed ... FAIL
s3tests_boto3.functional.test_s3.test_object_raw_get ... ok
s3tests_boto3.functional.test_s3.test_object_raw_get_bucket_gone ... FAIL
s3tests_boto3.functional.test_s3.test_object_delete_key_bucket_gone ... FAIL
s3tests_boto3.functional.test_s3.test_object_raw_get_object_gone ... ok
s3tests_boto3.functional.test_s3.test_object_raw_authenticated ... ok
s3tests_boto3.functional.test_s3.test_object_raw_response_headers ... ok
s3tests_boto3.functional.test_s3.test_object_raw_authenticated_bucket_acl ... ok
s3tests_boto3.functional.test_s3.test_object_raw_authenticated_object_acl ... ok
s3tests_boto3.functional.test_s3.test_object_raw_authenticated_bucket_gone ... FAIL
s3tests_boto3.functional.test_s3.test_object_raw_authenticated_object_gone ... ok
s3tests_boto3.functional.test_s3.test_object_raw_get_x_amz_expires_not_expired ... ok
s3tests_boto3.functional.test_s3.test_object_raw_get_x_amz_expires_out_range_zero ... FAIL
s3tests_boto3.functional.test_s3.test_object_raw_get_x_amz_expires_out_max_range ... FAIL
s3tests_boto3.functional.test_s3.test_object_raw_get_x_amz_expires_out_positive_range ... FAIL
s3tests_boto3.functional.test_s3.test_object_anon_put ... FAIL
s3tests_boto3.functional.test_s3.test_object_anon_put_write_access ... ok
s3tests_boto3.functional.test_s3.test_object_put_authenticated ... ok
s3tests_boto3.functional.test_s3.test_object_raw_put_authenticated_expired ... FAIL
s3tests_boto3.functional.test_s3.test_object_acl_canned_publicreadwrite ... ERROR
s3tests_boto3.functional.test_s3.test_object_acl ... ERROR
s3tests_boto3.functional.test_s3.test_object_acl_write ... ERROR
s3tests_boto3.functional.test_s3.test_object_acl_writeacp ... ERROR
s3tests_boto3.functional.test_s3.test_object_acl_read ... ERROR
s3tests_boto3.functional.test_s3.test_object_acl_readacp ... ERROR
s3tests_boto3.functional.test_s3.test_object_header_acl_grants ... ERROR
s3tests_boto3.functional.test_s3.test_access_bucket_private_object_private ... FAIL
s3tests_boto3.functional.test_s3.test_access_bucket_private_objectv2_private ... FAIL
s3tests_boto3.functional.test_s3.test_access_bucket_private_object_publicread ... FAIL
s3tests_boto3.functional.test_s3.test_access_bucket_private_objectv2_publicread ... FAIL
s3tests_boto3.functional.test_s3.test_access_bucket_private_object_publicreadwrite ... FAIL
s3tests_boto3.functional.test_s3.test_access_bucket_private_objectv2_publicreadwrite ... FAIL
s3tests_boto3.functional.test_s3.test_access_bucket_publicread_object_private ... ERROR
s3tests_boto3.functional.test_s3.test_access_bucket_publicread_object_publicread ... ERROR
s3tests_boto3.functional.test_s3.test_access_bucket_publicread_object_publicreadwrite ... ERROR
s3tests_boto3.functional.test_s3.test_access_bucket_publicreadwrite_object_private ... ERROR
s3tests_boto3.functional.test_s3.test_access_bucket_publicreadwrite_object_publicread ... ERROR
s3tests_boto3.functional.test_s3.test_access_bucket_publicreadwrite_object_publicreadwrite ... ERROR
s3tests_boto3.functional.test_s3.test_bucket_create_special_key_names ... ok
s3tests_boto3.functional.test_s3.test_object_copy_zero_size ... ok
s3tests_boto3.functional.test_s3.test_object_copy_same_bucket ... ok
s3tests_boto3.functional.test_s3.test_object_copy_verify_contenttype ... FAIL
s3tests_boto3.functional.test_s3.test_object_copy_to_itself ... ok
s3tests_boto3.functional.test_s3.test_object_copy_to_itself_with_metadata ... ok
s3tests_boto3.functional.test_s3.test_object_copy_diff_bucket ... ok
s3tests_boto3.functional.test_s3.test_object_copy_not_owned_bucket ... FAIL
s3tests_boto3.functional.test_s3.test_object_copy_not_owned_object_bucket ... ERROR
s3tests_boto3.functional.test_s3.test_object_copy_canned_acl ... ok
s3tests_boto3.functional.test_s3.test_object_copy_retaining_metadata ... FAIL
s3tests_boto3.functional.test_s3.test_object_copy_replacing_metadata ... ok
s3tests_boto3.functional.test_s3.test_object_copy_bucket_not_found ... ok
s3tests_boto3.functional.test_s3.test_object_copy_key_not_found ... ok
s3tests_boto3.functional.test_s3.test_multipart_upload_empty ... ok
s3tests_boto3.functional.test_s3.test_multipart_upload_small ... ERROR
s3tests_boto3.functional.test_s3.test_multipart_copy_small ... ok
s3tests_boto3.functional.test_s3.test_multipart_copy_invalid_range ... FAIL
s3tests_boto3.functional.test_s3.test_multipart_copy_improper_range ... FAIL
s3tests_boto3.functional.test_s3.test_multipart_copy_without_range ... ok
s3tests_boto3.functional.test_s3.test_multipart_copy_special_names ... ok
s3tests_boto3.functional.test_s3.test_multipart_upload ... ERROR
s3tests_boto3.functional.test_s3.test_multipart_upload_resend_part ... ok
s3tests_boto3.functional.test_s3.test_multipart_upload_size_too_small ... FAIL
s3tests_boto3.functional.test_s3.test_multipart_upload_contents ... ok
s3tests_boto3.functional.test_s3.test_multipart_upload_overwrite_existing_object ... ok
s3tests_boto3.functional.test_s3.test_abort_multipart_upload ... ok
s3tests_boto3.functional.test_s3.test_abort_multipart_upload_not_found ... ok
s3tests_boto3.functional.test_s3.test_list_multipart_upload ... ok
s3tests_boto3.functional.test_s3.test_multipart_upload_missing_part ... ok
s3tests_boto3.functional.test_s3.test_multipart_upload_incorrect_etag ... ok
s3tests_boto3.functional.test_s3.test_100_continue ... FAIL
s3tests_boto3.functional.test_s3.test_atomic_read_1mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_read_4mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_read_8mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_write_1mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_write_4mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_write_8mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_dual_write_1mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_dual_write_4mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_dual_write_8mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_conditional_write_1mb ... ok
s3tests_boto3.functional.test_s3.test_atomic_dual_conditional_write_1mb ... FAIL
s3tests_boto3.functional.test_s3.test_atomic_write_bucket_gone ... ok
s3tests_boto3.functional.test_s3.test_atomic_multipart_upload_write ... ok
s3tests_boto3.functional.test_s3.test_multipart_resend_first_finishes_last ... ok
s3tests_boto3.functional.test_s3.test_ranged_request_response_code ... ok
s3tests_boto3.functional.test_s3.test_ranged_big_request_response_code ... ok
s3tests_boto3.functional.test_s3.test_ranged_request_skip_leading_bytes_response_code ... ok
s3tests_boto3.functional.test_s3.test_ranged_request_return_trailing_bytes_response_code ... ok
s3tests_boto3.functional.test_s3.test_ranged_request_invalid_range ... ok
s3tests_boto3.functional.test_s3.test_ranged_request_empty_object ... ok
s3tests_boto3.functional.test_s3.test_get_obj_tagging ... ok
s3tests_boto3.functional.test_s3.test_get_obj_head_tagging ... ok
s3tests_boto3.functional.test_s3.test_put_max_tags ... ok
s3tests_boto3.functional.test_s3.test_put_excess_tags ... ok
s3tests_boto3.functional.test_s3.test_put_max_kvsize_tags ... ok
s3tests_boto3.functional.test_s3.test_put_excess_key_tags ... ok
s3tests_boto3.functional.test_s3.test_put_excess_val_tags ... ok
s3tests_boto3.functional.test_s3.test_put_modify_tags ... ok
s3tests_boto3.functional.test_s3.test_put_delete_tags ... ok
s3tests_boto3.functional.test_s3.test_post_object_tags_anonymous_request ... FAIL
s3tests_boto3.functional.test_s3.test_post_object_tags_authenticated_request ... FAIL
s3tests_boto3.functional.test_s3.test_put_obj_with_tags ... ok
s3tests_boto3.functional.test_s3.test_object_lock_multi_delete_object_with_retention ... ERROR
s3tests_boto3.functional.test_s3.test_object_lock_changing_mode_from_governance_with_bypass ... ok
s3tests_boto3.functional.test_s3.test_object_lock_changing_mode_from_governance_without_bypass ... FAIL
s3tests_boto3.functional.test_s3.test_object_lock_changing_mode_from_compliance ... FAIL
s3tests_boto3.functional.test_s3.test_copy_object_ifmatch_good ... ok
s3tests_boto3.functional.test_s3.test_copy_object_ifmatch_failed ... FAIL
s3tests_boto3.functional.test_s3.test_copy_object_ifnonematch_good ... FAIL
s3tests_boto3.functional.test_s3.test_copy_object_ifnonematch_failed ... ok
s3tests_boto3.functional.test_s3.test_object_read_unreadable ... FAIL
ERROR

======================================================================
ERROR: s3tests_boto3.functional.test_s3.test_bucket_list_return_data
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/s3-tests/virtualenv/lib/python3.6/site-packages/nose/case.py", line 198, in runTest
    self.test(*self.arg)
  File "/s3-tests/s3tests_boto3/functional/test_s3.py", line 1669, in test_bucket_list_return_data
    'DisplayName': acl_response['Owner']['DisplayName'],
KeyError: 'Owner'
-------------------- >> begin captured logging << --------------------
```
