<main>
<h1>Common Provenance Model RO-Crate profile</h1>
<p>Research objects, such as data, experimental results, computational models, or
        biological samples, are exchanged between organizations, so each of the organizations can provide provenance
        information only about a part of the research object&rsquo;s life cycle. As a result, a complete provenance
        description of the object is then spread across different heterogeneous organizations. The Common Provenance
        Model (CPM) provides a baseline for such distributed provenance chains. It defines how to interconnect
        distributed provenance parts encapsulated in PROV bundles, how to express standardized derivation paths
        between inputs and outputs of a process in a single bundle (so called provenance backbone), and how to
        attach domain specific information to the chain in a harmonized way. </p>
<p></p>
<p>This document specifies how to identify and handle CPM compliant provenance files
        and CPM compliant meta-provenance files in an RO-Crate. </p>
<p></p>
<p>CPM Publication: <a
            href="https://doi.org/10.1038/s41597-022-01537-6">https://doi.org/10.1038/s41597-022-01537-6</a><span
       >&nbsp;</p>
<h3 id="h.f7xafzxfzqxj">General Requirements</h3>
<ul>
    <li>Each CPM compliant provenance bundle MUST be serialized into a
            standalone file. </li>
    <li>The RO-Crate MAY contain multiple CPM compliant bundles/files.
        </li>
    <li>The RO-Crate MUST include references to all CPM compliant
            provenance bundles/files present in the crate (arbitrary provenance files or log files do not need to be
            mentioned).</li>
</ul>
<ul>
    <li>Rationale: Each CPM provenance bundle is part of a distributed
            provenance chain. As a consequence, any such bundle can be referenced from other parts of the chain,
            which can be stored externally (outside the crate). For that reason, the RO-Crate must provide means to
            identify and locate any of the CPM compliant provenance bundles present in the crate. </li>
</ul>
<ul>
    <li>The RO-Crate MAY include a meta provenance file<span
           >. Multiple meta-provenance bundles MAY be present in the meta provenance file. </li>
</ul>
<ul>
    <li>Rationale: This is to keep meta provenance handling simple. If
            multiple meta provenance files would be allowed, then we would have to set requirements on how meta
            provenance can be split across the files, which might introduce unnecessary complexity.</li>
</ul>
<ul>
    <li>The RO Crate MUST include a reference to the meta provenance file,
            if present. </li>
</ul>
<p></p><a id="t.fd37530046dae0f22cfb0ad78e77fd5d4f09726f"></a><a id="t.0"></a>
<table>
    <tr>
        <td>
            <p>Type/Property<sup><a href="#ftnt1"
                        id="ftnt_ref1">[1]</a></sup></p>
        </td>
        <td>
            <p>Required?</p>
        </td>
        <td>
            <p>Description</p>
        </td>
    </tr>
    <tr>
        <td colspan="3">
            <p>CPMProvenanceFile<br>extends <span
                   ><a
                        href="https://www.google.com/url?q=http://schema.org/MediaObject&amp;sa=D&amp;source=editors&amp;ust=1673376421332497&amp;usg=AOvVaw3atbOCNWihvZbdcbOn1IMN">MediaObject</a><span
                   >&nbsp;(@id is resolvable), dataEntity </p>
        </td>
    </tr>
    <tr>
        <td>
            <p>@type</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Type that identifies the CPM provenance file.</p>
            <p>Array MUST include &quot;File&quot;. Array <span
                   >MUST include &nbsp;&ldquo;<span
                   >CPMProvenanceFile&rdquo;.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>@id</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Identifier of the CPM provenance file.</p>
            <p>SHOULD be a relative URI&nbsp;to a data entity
                    in the crate (e.g. &quot;provenance/prov-training.provn&quot;<span
                   >) but MAY be an absolute URI .
                    Resolving this identifier MUST
                    return this provenance file in the given format.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=https://schema.org/identifier&amp;sa=D&amp;source=editors&amp;ust=1673376421337675&amp;usg=AOvVaw3oCEca17M_2qvvDbyLsXaq">identifier</a>
            </p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>Identifier of a provenance bundle present in the CPM provenance file.
                </p>
            <p>MUST be an absolute URI. MUST match the expanded bundle
                    identifier<sup><a href="#ftnt2" id="ftnt_ref2">[2]</a></sup>.
                MAY be equal to @id if absolute. <sup><a href="#cmnt1"
                        id="cmnt_ref1">[a]</a></sup></p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=http://schema.org/dateModified&amp;sa=D&amp;source=editors&amp;ust=1673376421339784&amp;usg=AOvVaw3tfyeQ12_spbV1QCCf0ZAc">dateModified</a>
            </p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>The time this&nbsp;CPM
                provenance&nbsp;file was last modified/written
                    (not necessarily when the<span
                   >&nbsp;bundle&nbsp;included&nbsp;was
                finalized or the file was added to
                    the RO-Crate).</p>
            <p>MUST be a string with format &ldquo;ddMMYYYY&rdquo;.<sup><a href="#cmnt2"
                        id="cmnt_ref2">[b]</a></sup><sup><a href="#cmnt3" id="cmnt_ref3">[c]</a></sup></p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=http://schema.org/encodingFormat&amp;sa=D&amp;source=editors&amp;ust=1673376421342067&amp;usg=AOvVaw1JJnna_phm_GGZKYz7v0B1">encodingFormat</a>
            </p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Encoding of the CPM provenance file.</p>
            <p>Array MUST contain a string indicating the IANA media type of the file,
                    e.g. &quot;text/turtle&quot; or &quot;text/provenance-notation&quot; or
                    &quot;application/ld+json&quot;.</p>
            <p>Array MUST also contain a reference to a CreativeWork that indicates the
                    PROV format used in the serialization. &quot;@id&quot; SHOULD be one of:</p>
            <ul>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/REC-prov-n-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421343794&amp;usg=AOvVaw1RxhC3lQhKUmtNS7KlCzak">http://www.w3.org/TR/2013/REC-prov-n-20130430/</a><span
                       >&nbsp;(PROV-N)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/REC-prov-o-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421344331&amp;usg=AOvVaw36tDlfNMsd7fxz3PnqeDKE">http://www.w3.org/TR/2013/REC-prov-o-20130430/</a><span
                       >&nbsp;(PROV-O as RDF or OWL)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/NOTE-prov-xml-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421344886&amp;usg=AOvVaw0Xetbi85HDcYo_FXwv9cTk">http://www.w3.org/TR/2013/NOTE-prov-xml-20130430/</a><span
                       >&nbsp;(PROV-XML)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/Submission/2013/SUBM-prov-json-20130424/&amp;sa=D&amp;source=editors&amp;ust=1673376421345508&amp;usg=AOvVaw1JKrufl11TgtMqkKsU59nA">http://www.w3.org/Submission/2013/SUBM-prov-json-20130424/</a><span
                       >&nbsp;(PROV-JSON)</li>
            </ul>
            <p>Example:</p>
            <p>{ &ldquo;@id: &ldquo;provone.ttl&rdquo;, &ldquo;@type&rdquo;
                    [&ldquo;File&rdquo;, &rdquo;CPMProvenanceFile&rdquo;],</p>
            <p>&ldquo;encodingFormat&rdquo;: [<br>
                    &nbsp;&ldquo;text/turtle&rdquo;,<br> &nbsp;{&ldquo;@id&rdquo;:
                    &ldquo;http://www.w3.org/TR/2013/REC-prov-o-20130430/&rdquo;}<br>]</p>
            <p>{&ldquo;@id&rdquo;:
                    &ldquo;http://www.w3.org/TR/2013/REC-prov-o-20130430/&rdquo;,<br>&ldquo;@type&rdquo;:
                    &ldquo;CreativeWork&rdquo;}</p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=http://schema.org/about&amp;sa=D&amp;source=editors&amp;ust=1673376421347212&amp;usg=AOvVaw0QyLjzr0i8oGCNqCTDeZHt">about</a>
            </p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>Array contains entity identifiers, which are documented by the CPM
                    provenance file. <sup><a href="#cmnt4" id="cmnt_ref4">[d]</a></sup></p>
            <p>SHOULD contain at least one identifier. </p>
        </td>
    </tr>
    <tr>
        <td colspan="3">
            <p>CPMMetaProvenanceFile<br>extends
                    CPMProvenanceFile</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>@type</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Type that identifies the CPM meta provenance file.</p>
            <p>Array MUST include &quot;File&quot;. MUST include
                    CPMMetaProvenanceFile</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>@id</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Identifier of the CPM meta provenance file.</p>
            <p>SHOULD be an absolute URI , but MAY be a relative URI to a data entity
                    in the crate (e.g. &quot;provenance/prov-meta.jsonld&quot;<span
                   >) </p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=http://schema.org/dateModified&amp;sa=D&amp;source=editors&amp;ust=1673376421353239&amp;usg=AOvVaw2HwJO2_MdyYGH6XuQcn9K_">dateModified</a>
            </p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>The time this CPM meta provenance file was last modified/written (not
                    necessarily when the bundle included was finalized or the file was added to the
                    RO-Crate).</p>
            <p>MUST be a string with format &ldquo;ddMMYYYY&rdquo;.<sup><a href="#cmnt5"
                        id="cmnt_ref5">[e]</a></sup></p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=http://schema.org/encodingFormat&amp;sa=D&amp;source=editors&amp;ust=1673376421355346&amp;usg=AOvVaw3eHKSO9wyIAjy9dFydb8Wv">encodingFormat</a>
            </p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Encoding of the CPM meta provenance file.</p>
            <p>Array MUST contain a string indicating the IANA media type of the file,
                    e.g. &quot;text/turtle&quot; or &quot;text/provenance-notation&quot; or
                    &quot;application/ld+json&quot;.</p>
            <p>Array MUST also contain a reference to a CreativeWork that indicates the
                    PROV format used in the serialization. &quot;@id&quot; SHOULD be one of:</p>
            <ul>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/REC-prov-n-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421357009&amp;usg=AOvVaw3mGAn-Xq_3adM2PLsqolSu">http://www.w3.org/TR/2013/REC-prov-n-20130430/</a><span
                       >&nbsp;(PROV-N)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/REC-prov-o-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421357537&amp;usg=AOvVaw13R8rko17zNLDxds90yzno">http://www.w3.org/TR/2013/REC-prov-o-20130430/</a><span
                       >&nbsp;(PROV-O as RDF or OWL)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/NOTE-prov-xml-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421358024&amp;usg=AOvVaw1zDlQenvha6bj7jqUbH0bl">http://www.w3.org/TR/2013/NOTE-prov-xml-20130430/</a><span
                       >&nbsp;(PROV-XML)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/Submission/2013/SUBM-prov-json-20130424/&amp;sa=D&amp;source=editors&amp;ust=1673376421358472&amp;usg=AOvVaw03zWYWh5lUFuyzGTLi0hui">http://www.w3.org/Submission/2013/SUBM-prov-json-20130424/</a><span
                       >&nbsp;(PROV-JSON)</li>
            </ul>
            <p>Example:</p>
            <p>{ &ldquo;@id: &ldquo;provone.ttl&rdquo;, &ldquo;@type&rdquo;
                    [&ldquo;File&rdquo;, &rdquo;CPMProvenanceFile&rdquo;],</p>
            <p>&ldquo;encodingFormat&rdquo;: [<br>
                    &nbsp;&ldquo;text/turtle&rdquo;,<br> &nbsp;{&ldquo;@id&rdquo;:
                    &ldquo;http://www.w3.org/TR/2013/REC-prov-o-20130430/&rdquo;}<br>]</p>
            <p>{&ldquo;@id&rdquo;:
                    &ldquo;http://www.w3.org/TR/2013/REC-prov-o-20130430/&rdquo;,<br>&ldquo;@type&rdquo;:
                    &ldquo;CreativeWork&rdquo;}</p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=http://schema.org/hasPart&amp;sa=D&amp;source=editors&amp;ust=1673376421360601&amp;usg=AOvVaw1qdlrAvrFRQuKDmMve6qUf">hasPart</a><sup><a
                        href="#cmnt6" id="cmnt_ref6">[f]</a></sup></p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Identifiers of meta provenance bundles present in the CPM meta
                    provenance file. </p>
            <p>Array MUST contain absolute URIs. URIs MUST match the expanded bundle
                    identifiers as used internally in the CPM provenance files. </p>
        </td>
    </tr>
</table>
<p></p>
<h2 id="h.sn4o0wzhwnu8">Example</h2>
<p>The example RO-Crate documents a single step computation implemented as a python
        script which takes a file as input and generates another file as output. In addition, the computation
        generated an arbitrary log file, which was transformed into a CPM compliant provenance bundle using a
        standalone python script. The resulting CPM provenance file documents the computation execution. </p>
<p></p>
<p>{ &quot;@context&quot;: [&quot;<a
            href="https://www.google.com/url?q=https://w3id.org/ro/crate/1.1/context&amp;sa=D&amp;source=editors&amp;ust=1673376421364476&amp;usg=AOvVaw27YxhDoNUS1lP6nRabm2lP">https://w3id.org/ro/crate/1.1/context</a><span
       >&quot;,<sup><a href="#cmnt7" id="cmnt_ref7">[g]</a></sup><sup><a href="#cmnt8"
            id="cmnt_ref8">[h]</a></sup></p>
<p>&nbsp; { &quot;CPMProvenanceFile&quot;:
        &quot;https://w3id.org/ro/terms/cpm#CPMProvenanceFile&quot;,</p>
<p>&nbsp; &nbsp; &quot;CPMMetaProvenanceFile&quot;:
        &quot;https://w3id.org/ro/terms/cpm#CPMMetaProvenanceFile&quot;,</p>
<p>&nbsp; ],</p>
<p>&nbsp; &quot;@graph&quot;: [</p>
<p></p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp; &quot;@type&quot;: &quot;CreativeWork&quot;,</p>
<p>&nbsp; &nbsp; &quot;@id&quot;: &quot;ro-crate-metadata.json&quot;,</p>
<p>&nbsp; &nbsp; &quot;conformsTo&quot;: {&quot;@id&quot;:
        &quot;https://w3id.org/ro/crate/1.1&quot;},</p>
<p>&nbsp; &nbsp; &quot;about&quot;: {&quot;@id&quot;: &quot;./&quot;}</p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp; &quot;@id&quot;: &quot;./&quot;,</p>
<p>&nbsp; &nbsp; &quot;@type&quot;: &quot;Dataset&quot;,</p>
<p>&nbsp; &nbsp; &quot;datePublished&quot;: &quot;2022&quot;,</p>
<p>&nbsp; &nbsp; &quot;conformsT<sup><a href="#cmnt9"
            id="cmnt_ref9">[i]</a></sup><sup><a href="#cmnt10" id="cmnt_ref10">[j]</a></sup><sup><a href="#cmnt11"
            id="cmnt_ref11">[k]</a></sup>o&quot;: [</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp;{&quot;@id&quot;: &quot;<a
           
            href="https://www.google.com/url?q=https://w3id.org/ro/wfrun/0.1/process&amp;sa=D&amp;source=editors&amp;ust=1673376421368578&amp;usg=AOvVaw0exP1i9G_GFv8AAomq1Q4I">https://w3id.org/ro/wfrun/0.1/process</a><span
       >&quot;<sup><a href="#cmnt12" id="cmnt_ref12">[l]</a></sup><sup><a href="#cmnt13"
            id="cmnt_ref13">[m]</a></sup><sup><a href="#cmnt14" id="cmnt_ref14">[n]</a></sup><sup><a href="#cmnt15"
            id="cmnt_ref15">[o]</a></sup><sup><a href="#cmnt16" id="cmnt_ref16">[p]</a></sup><sup><a href="#cmnt17"
            id="cmnt_ref17">[q]</a></sup><span
       >},<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&quot;@id&quot;: &quot;<span
       >https://w3id.org/cpm/crate/0.1??&quot;<sup><a href="#cmnt18"
            id="cmnt_ref18">[r]</a></sup><sup><a href="#cmnt19" id="cmnt_ref19">[s]</a></sup><sup><a href="#cmnt20"
            id="cmnt_ref20">[t]</a></sup><sup><a href="#cmnt21" id="cmnt_ref21">[u]</a></sup><sup><a href="#cmnt22"
            id="cmnt_ref22">[v]</a></sup><sup><a href="#cmnt23" id="cmnt_ref23">[w]</a></sup>},
</p>
<p>&nbsp; &nbsp; ],</p>
<p>&nbsp; &nbsp; &quot;name&quot;: &quot;&quot;,</p>
<p>&nbsp; &nbsp; &quot;description&quot;: &quot;&quot;,</p>
<p>&nbsp; &nbsp; &quot;hasPart&quot;: [</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &quot;@id&quot;: &quot;INPUT_DATASET_PATH&quot;
</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; },</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &quot;@id&quot;:
        &quot;OUTPUT_DATASET_PATH&quot;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; },</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &quot;@id&quot;:
        &quot;COMPUTATION_LOG_FILE&quot;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; },</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &quot;@id&quot;:
        &quot;CPM_COMPLIANT_PROVENANCE&quot;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; },</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &quot;@id&quot;:
        &quot;COMPUTATION_SCRIPT&quot;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; },</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &quot;@id&quot;:
        &quot;CPM_PROVENANCE_GENERATION_SCRIPT&quot;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; }</p>
<p>&nbsp; &nbsp; &nbsp; ],</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;<span
       >mentions&quot;: [</p>
<p><span
       >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
        &quot;@id&quot;: &quot;#Exec-computation&quot;},</p>
<p><span
       >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{
        &quot;@id&quot;: &quot;#Exec-CPM-provgen&quot;}</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]</p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp;&quot;@id&quot;: &quot;<span
       >INPUT_DATASET_PATH<sup><a href="#cmnt24" id="cmnt_ref24">[x]</a></sup><span
       >&quot;,</p>
<p>&nbsp; &nbsp;&quot;@type&quot;: &quot;File&quot;,</p>
<p>&nbsp; &nbsp;&quot;description&quot;: &quot;&quot;,</p>
<p>&nbsp; &nbsp;&quot;name&quot;: &quot;&quot;</p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp;&quot;@id&quot;: &quot;OUTPUT_DATASET_PATH&quot;,</p>
<p>&nbsp; &nbsp;&quot;@type&quot;: &quot;File&quot;,</p>
<p>&nbsp; &nbsp;&quot;description&quot;: &quot;&quot;,</p>
<p>&nbsp; &nbsp;&quot;name&quot;: &quot;&quot;</p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp;&quot;@id&quot;: &quot;COMPUTATION_SCRIPT&quot;,</p>
<p>&nbsp; &nbsp;&quot;@type&quot;:
        [&quot;File&quot;,&quot;SoftwareSourceCode&quot;],</p>
<p>&nbsp; &nbsp;&quot;description&quot;: &quot;&quot;,</p>
<p>&nbsp; &nbsp;&quot;name&quot;: &quot;&quot;</p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp;&quot;@id&quot;: &quot;COMPUTATION_LOG_FILE&quot;,</p>
<p>&nbsp; &nbsp;&quot;@type&quot;: &quot;File&quot;,</p>
<p>&nbsp; &nbsp;&quot;description&quot;: &quot;A log file generated by the
        computation</p>
<p>&nbsp;execution.&quot;,</p>
<p>&nbsp; &nbsp;&quot;name&quot;: &quot;&quot;</p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp;&quot;@id&quot;: &quot;CPM_PROVENANCE_GENERATION_SCRIPT&quot;,
</p>
<p>&nbsp; &nbsp;&quot;@type&quot;:
        [&quot;File&quot;,&quot;SoftwareSourceCode&quot;],</p>
<p>&nbsp; &nbsp;&quot;description&quot;: &quot;A python script that translates the
        computation log</p>
<p>&nbsp;files into CPM compliant provenance file.&quot;,</p>
<p>&nbsp; &nbsp;&quot;name&quot;: &quot;&quot;</p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp;&quot;@id&quot;: &quot;<span
       >CPM_COMPLIANT_PROVENANCE&quot;,</p>
<p>&nbsp; &nbsp;&quot;@type&quot;: [&quot;File&quot;,
        &quot;CPMProvenanceFile&quot;],</p>
<p>&nbsp; &nbsp;&quot;description&quot;: &quot;CPM compliant provenance file generated
        based on </p>
<p>the computation log file.&quot;,</p>
<p>&nbsp; &nbsp;&quot;encodingFormat&quot;: [</p>
<p><span
       >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;text/provenance-notation&quot;,</p>
<p>{ &quot;@id&quot;:
        &quot;http://www.w3.org/TR/2013/REC-prov-n-20130430/&quot;<sup><a href="#cmnt25"
            id="cmnt_ref25">[y]</a></sup><sup><a href="#cmnt26" id="cmnt_ref26">[z]</a></sup><sup><a href="#cmnt27"
            id="cmnt_ref27">[aa]</a></sup>},</p>
<p>&nbsp; &nbsp;&quot;name<sup><a href="#cmnt28"
            id="cmnt_ref28">[ab]</a></sup><sup><a href="#cmnt29" id="cmnt_ref29">[ac]</a></sup><sup><a href="#cmnt30"
            id="cmnt_ref30">[ad]</a></sup><sup><a href="#cmnt31" id="cmnt_ref31">[ae]</a></sup><sup><a href="#cmnt32"
            id="cmnt_ref32">[af]</a></sup><sup><a href="#cmnt33" id="cmnt_ref33">[ag]</a></sup>&quot;:
        &quot;&quot;,</p>
<p>&nbsp; &nbsp;&quot;about&quot;: [{&quot;@id&quot;:
        &quot;#Exec-computation&quot;}]</p>
<p></p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp;&quot;@id&quot;: &quot;#Exec-computation&quot;,</p>
<p>&nbsp; &nbsp;&quot;@type&quot;: [&quot;CreateAction&quot;],</p>
<p>&nbsp; &nbsp;&quot;description&quot;: &quot;Computation execution.&quot;,</p>
<p>&nbsp; &nbsp;&quot;name&quot;: &quot;&quot;,</p>
<p>&nbsp; &nbsp; &quot;instrument&quot;: {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &quot;@id&quot;:
        &quot;COMPUTATION_SCRIPT&quot;</p>
<p>&nbsp; &nbsp; },</p>
<p>&nbsp; &nbsp; &quot;object&quot;: [</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; {&quot;@id&quot;:
        &quot;INPUT_DATASET_PATH&quot;}</p>
<p>&nbsp; &nbsp; ],</p>
<p>&nbsp; &nbsp; &quot;result&quot;: [</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; {&quot;@id&quot;:
        &quot;OUTPUT_DATASET_PATH&quot;},</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; {&quot;@id&quot;:
        &quot;COMPUTATION_LOG_FILE&quot;}</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; ]</p>
<p>&nbsp;},</p>
<p>&nbsp;{</p>
<p>&nbsp; &nbsp;&quot;@id&quot;: &quot;#Exec-CPM-provgen&quot;,</p>
<p>&nbsp; &nbsp;&quot;@type&quot;: [&quot;CreateAction&quot;],</p>
<p>&nbsp; &nbsp;&quot;description&quot;: &quot;CPM compliant provenance
        generation.&quot;,</p>
<p>&nbsp; &nbsp;&quot;name&quot;: &quot;&quot;,</p>
<p>&nbsp; &nbsp;&quot;instrument&quot;: {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &quot;@id&quot;:
        &quot;CPM_PROVENANCE_GENERATION_SCRIPT&quot;</p>
<p>&nbsp; &nbsp; &nbsp; },</p>
<p>&nbsp; &nbsp; &quot;object&quot;: [</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; {&quot;@id&quot;:
        &quot;COMPUTATION_LOG_FILE&quot;}</p>
<p>&nbsp; &nbsp; ],</p>
<p>&nbsp; &nbsp; &quot;result&quot;: [</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; {&quot;@id&quot;:
        &quot;CPM_COMPLIANT_PROVENANCE&quot;}</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; ]</p>
<p>&nbsp;}</p>
<p>&nbsp;]</p>
<p>}</p>
<h2 id="h.incsjr9qwpbo">Obsolete notes</h2>
<p>For the implementation of case 1) (provenance is provided to consumers in an
        original storage format), we have chosen RO-Crates<sup><a href="#ftnt3"
            id="ftnt_ref3">[3]</a></sup>. RO Crate is &hellip; In our implementation, we take an
        existing AI based computational workflow implemented as a set of python scripts, express the computational
        results using RO-Crate, generate provenance information in accordance with the specification of RO Crate and
        the extension of the CPM. </p>
<p>According to the common provenance model, the resulting provenance must contain
        a meta-bundle. In this case, the meta bundle documents the history of three <span
       >root bundles, each of them describing a standalone part of the
        AI workflow - data preprocessing, model training, model testing. </p>
<p><a
            href="https://www.google.com/url?q=https://drive.google.com/drive/folders/1VO82z0YKX6lVucJXfDXe3ldF3JOXB34S?usp%3Dsharing&amp;sa=D&amp;source=editors&amp;ust=1673376421390857&amp;usg=AOvVaw1vGyDpD0nTaEFdkSEIU7cn">Link
            to the RO Crate</a>.</p>
<p>Since RO Crates primarily work on a file system level, the most natural way to
        express a bundle in an RO Crate is to serialize each bundle into a separate file<sup><a
            href="#ftnt4" id="ftnt_ref4">[4]</a></sup>. This allows a natural
        mapping between the RO Crate&rsquo;s data item properties and bundles. </p>
<p>As a result, each RO-Crate must contain:</p>
<ol start="1">
    <li>Do we also want to include the identifier of a bundle in the
            RO crate? This might be necessary if we allow multiple bundles in a single file, to enable references to
            a specific bundle. This specification also does not cover cases when (for instance) we have provn with 2
            named bundles and one top-level-instance bundle. </li>
</ol>
<p></p>
<h3 id="h.7c7eo6l3qlmo">General Requirements</h3><a
    id="t.f9f0bab8ee040aef8effdad2ce0bb29b0df2bd2a"></a><a id="t.1"></a>
<table>
    <tr>
        <td>
            <p>Type/Property<sup><a href="#ftnt5"
                        id="ftnt_ref5">[5]</a></sup></p>
        </td>
        <td>
            <p>Required?</p>
        </td>
        <td>
            <p>Description</p>
        </td>
    </tr>
    <tr>
        <td colspan="3">
            <p>CPMProvenanceFile<br>extends
                <a
                        href="https://www.google.com/url?q=http://schema.org/MediaObject&amp;sa=D&amp;source=editors&amp;ust=1673376421396081&amp;usg=AOvVaw3waP6VBOAkxvliyvYIkZQk">MediaObject</a><span
                   >&nbsp;(@id is resolvable), dataEntity </p>
        </td>
    </tr>
    <tr>
        <td>
            <p>@type</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Array MUST include &quot;File&quot;. MUST include
                    &nbsp;CPMProvenanceFile or its subtype CPMMetaProvenanceFile</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>@id</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>SHOULD be an absolute URI but MAY be a relative URI to a data
                    entity in the crate (e.g. <span
                   >&quot;provenance/prov-training.provn&quot;). Resolving
                    this identifier MUST return this provenance file in the given format.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=https://schema.org/identifier&amp;sa=D&amp;source=editors&amp;ust=1673376421402712&amp;usg=AOvVaw3A4cF-DUMripo5Wq_YawB9">identifier</a>
            </p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>If this provenance file contains only a single fragment or meta
                    bundle, then this property MUST be present. <br><br>If present:<br>MUST be absolute URI. MUST
                    match expanded bundle identifier as defined within the meta-bundle provenance<sup
                   ><a href="#ftnt6" id="ftnt_ref6">[6]</a></sup>. MAY be equal to
                    @id if absolute. </p>
            <p>If not present: property hasPart must be specified.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=https://schema.org/hasPart&amp;sa=D&amp;source=editors&amp;ust=1673376421405534&amp;usg=AOvVaw0rn3uuZzicvB_yDmQIU3cj">hasPart</a><span
                   >&nbsp;</p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>If this provenance file contains more than one fragment bundle, then
                    this property MUST be present to identify them. </p>
            <p>If present, each of the members:<br>MUST be absolute URI. MUST match
                    expanded bundle identifier as defined within the meta-bundle provenance. </p>
        </td>
    </tr>
    <tr>
        <td>
            <p>fileHash</p><sup><a href="#cmnt34" id="cmnt_ref34">[ah]</a></sup>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>0 or more PropertyValue (placeholder for file content checksum, to be
                    decided). Producers who are updating the provenance file MUST update or remove this
                    property.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>dateModified</p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>The time this provenance file was last modified/written (not
                    necessarily when its bundles were finalized or the file was added to the RO-Crate)</p>
        </td>
    </tr>
    <tr>
        <td>
            <p><a
                        href="https://www.google.com/url?q=http://schema.org/encodingFormat&amp;sa=D&amp;source=editors&amp;ust=1673376421410917&amp;usg=AOvVaw1iBM1K-3VrMpOcfCy36N9F">encodingFormat</a>
            </p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Array MUST contain a string indicate the IANA media type of the file,
                    e.g. &quot;text/turtle&quot; or &quot;text/provenance-notation&quot; or
                    &quot;application/ld+json&quot;.</p>
            <p>Array MUST also contain a reference to CreativeWork that indicates the
                    PROV format used in the serialization. &quot;@id&quot; SHOULD be one of:</p>
            <ul>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/REC-prov-n-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421413038&amp;usg=AOvVaw0dXKEcqnIMuCEAIbXeVFqH">http://www.w3.org/TR/2013/REC-prov-n-20130430/</a><span
                       >&nbsp;(PROV-N)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/REC-prov-o-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421413828&amp;usg=AOvVaw3mYIaIwTyNX3-KogupJGho">http://www.w3.org/TR/2013/REC-prov-o-20130430/</a><span
                       >&nbsp;(PROV-O as RDF or OWL)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/TR/2013/NOTE-prov-xml-20130430/&amp;sa=D&amp;source=editors&amp;ust=1673376421414384&amp;usg=AOvVaw1b3-QO1hBD5A1gWT9DHPfT">http://www.w3.org/TR/2013/NOTE-prov-xml-20130430/</a><span
                       >&nbsp;(PROV-XML)</li>
                <li><a
                            href="https://www.google.com/url?q=http://www.w3.org/Submission/2013/SUBM-prov-json-20130424/&amp;sa=D&amp;source=editors&amp;ust=1673376421414983&amp;usg=AOvVaw3nDvTQWR27cp8KRmPM_Cgz">http://www.w3.org/Submission/2013/SUBM-prov-json-20130424/</a><span
                       >&nbsp;(PROV-JSON)</li>
            </ul>
            <p>Example:</p>
            <p>{ &ldquo;@id: &ldquo;provone.ttl&rdquo;, &ldquo;@type&rdquo;
                    cpm:CPMProvenanceFile,</p>
            <p>&ldquo;encodingFormat&rdquo;: [<br>
                    &nbsp;&ldquo;text/turtle&rdquo;,<br> &nbsp;{&ldquo;@id&rdquo;:
                    &ldquo;http://www.w3.org/TR/2013/REC-prov-o-20130430/&rdquo;}<br>]</p>
            <p>{&ldquo;@id&rdquo;:
                    &ldquo;http://www.w3.org/TR/2013/REC-prov-o-20130430/&rdquo;,<br>&ldquo;@type&rdquo;:
                    &ldquo;CreativeWork&rdquo;}</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>conformsTo</p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>If this bundle has domain-specific provenance, conformsTo SHOULD point
                    to a CreativeWork that indicates the profile or domain-specific vocabulary used.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>&hellip;</p>
        </td>
        <td>
            <p></p>
        </td>
        <td>
            <p></p>
        </td>
    </tr>
    <tr>
        <td colspan="3">
            <p>CPMMetaProvenanceFile<br>extends
                    CPMProvenanceFile</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>@type</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Array MUST include &quot;File&quot;. MUST include
                    CPMMetaProvenanceFile</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>@id</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>SHOULD be an absolute URI , but MAY be a relative URI to a data
                    entity in the crate (e.g. <span
                   >&quot;provenance/prov-meta.jsonld&quot;) </p>
        </td>
    </tr>
    <tr>
        <td>
            <p></p>
        </td>
        <td>
            <p></p>
        </td>
        <td>
            <p>(same properties as for <span
                   >CPMProvenanceFile)</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>identifier</p>
        </td>
        <td>
            <p>SHOULD</p>
        </td>
        <td>
            <p>Be absolute URI that identify the meta
                    bundle&nbsp;that is contained by this
                    provenance file. </p>
        </td>
    </tr>
    <tr>
        <td>
            <p>hasPart</p>
        </td>
        <td>
            <p>SHOULD NOT</p>
        </td>
        <td>
            <p>Meta provenance files SHOULD NOT include other provenance
                    bundles.</p>
        </td>
    </tr>
    <tr>
        <td>
            <p>about</p>
        </td>
        <td>
            <p>MUST</p>
        </td>
        <td>
            <p>Array MUST list absolute URI of every <span
                   >root bundle&nbsp;which collection are defined
                    within the contained meta bundle(s). </p>
        </td>
    </tr>
</table>
<p></p>
<p></p>
<hr>
<div>
    <p><a href="#ftnt_ref1" id="ftnt1">[1]</a>&nbsp;The table structure
        copied from ro crate workflow run draft</p>
</div>
<div>
    <p><a href="#ftnt_ref2" id="ftnt2">[2]</a>&nbsp;PROV formats that support
            identified bundles SHOULD ensure their internally defined identifier also <span
           >matches&nbsp;this identifier.</p>
</div>
<div>
    <p><a href="#ftnt_ref3" id="ftnt3">[3]</a>&nbsp;<span
           ><a
                href="https://www.google.com/url?q=https://www.researchobject.org/ro-crate/&amp;sa=D&amp;source=editors&amp;ust=1673376421430662&amp;usg=AOvVaw3HatChQF2f0_CV-AZLOYrc">https://www.researchobject.org/ro-crate/</a><span
           >&nbsp;</p>
</div>
<div>
    <p><a href="#ftnt_ref4" id="ftnt4">[4]</a>&nbsp;Some PROV formats like PROV-N and
            PROV-O in JSON-LD support multiple bundles in the same document. This feature can be used if there is no
            need for different access control on different bundles.</p>
</div>
<div>
    <p><a href="#ftnt_ref5" id="ftnt5">[5]</a>&nbsp;The table structure
        copied from ro crate workflow run draft</p>
</div>
<div>
    <p><a href="#ftnt_ref6" id="ftnt6">[6]</a>&nbsp;PROV formats that support
            identified bundles SHOULD ensure their internally defined identifier also match this identifier.
    </p>
</div>
</main>