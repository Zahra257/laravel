    ****************web.php*********

 Route::controller(CouponsController::class)->prefix('Coupons')->group(function () {
            Route::get('', 'index')->name('Coupons'); //list
            Route::get('show/{id}', 'show')->name('Coupons.show'); //details
            Route::get('create', 'create')->name('Coupons.create'); //create
            Route::post('store', 'store')->name('Coupons.store');//save
            Route::get('edit/{id}', 'edit')->name('Coupons.edit'); 
            Route::patch('edit/{id}', 'update')->name('Coupons.update'); 
            Route::delete('destroy/{id}', 'destroy')->name('Coupons.destroy'); //sup
        });

**********sidbar**************
  <li class="nav-item">
                <a class="nav-link" href="{{ route('Coupons') }}">
                    <i class="fas fa-fw "></i>
                    <span>Coupons</span></a>
            </li>


********** view show.blade*******
@extends('layouts.app')

@section('title', 'Show Coupon')

@section('contents')
    <link href="{{ asset('admin_assets/mdb/css/mdb.min.css') }}" rel="stylesheet">
    <div class="row">
        <div class="col mx-auto mb-4">
            <div class="card mb-4">
              
                <div class="card-body">
                    <!-- Tabs navs -->
                   

                    <div class="tab-content" id="ex-with-icons-content">
                        <div class="tab-pane fade show active" id="ex-with-icons-tabs-1" role="tabpanel"
                            aria-labelledby="ex-with-icons-tab-1">
                            <div class="col">
                                    <div class="form-outline">
                                        <input type="text" id="code_coupon" name="code_coupon"
                                            class="form-control form-control-lg" value="{{ $Coupon->code_coupon }}" readonly
                                            required />
                                        <label class="form-label" for="code_coupon">Code coupon</label>
                                    </div>
                            <!-- 2 column grid layout with text inputs for the first and last names -->
                            <div class="row mb-4">
                                
                                </div>
                                <div class="row mb-4">
                                <div class="col">
                                    <div class="form-outline">
                                        <input type="text" id="Description" name="description"
                                            class="form-control form-control-lg" value="{{ $Coupon->description }}" readonly
                                            required />
                                        <label class="form-label" for="Description">Description</label>
                                    </div>
                                </div>
                                <div class="col">
                                    <div class="form-outline">
                                        <input type="text" id="lastname" name="lastname"
                                            class="form-control form-control-lg" value="{{ $Coupon->limit }}" readonly
                                            required />
                                        <label class="form-label" for="lastname">Limit</label>
                                    </div>
                                </div>
                            </div>

                          
                            <!-- Text input -->
                            <!-- Message input -->
                            <div class="row mb-4">
                                
                                <div class="col">
                                    <div class="form-outline">
                                        <input type="text" id="indicator" name="indicator"
                                            class="form-control form-control-lg" value="{{ $Coupon->date_debut }}" readonly
                                            required />
                                        <label class="form-label" for="indicator">Date Debut</label>
                                    </div>
                                </div>
                                <div class="col">
                                    <div class="form-outline">
                                        <input type="text" id="indicator" name="indicator"
                                            class="form-control form-control-lg" value="{{ $Coupon->date_fin }}" readonly
                                            required />
                                        <label class="form-label" for="indicator">Date fin</label>
                                    </div>
                                </div>
                            </div>
                         

                       
                    </div>



                </div>
            </div>
        </div>
    </div>
    <script src="{{ asset('admin_assets/mdb/js/mdb.min.js') }}"></script>
@endsection

*********** index.blade ************
@extends('layouts.app')

@section('title', 'Home Coupons')
@section('contents')
<link href="{{ asset('admin_assets/mdb/css/mdb.min.css') }}" rel="stylesheet">
<!-- DataTales Example -->
<div class="card shadow mb-4">
    <div class="card-header py-3">
        <div class="d-flex align-items-center justify-content-between">
            <div class="input-group rounded w-50">
                <input type="search" class="form-control rounded" id="datatable-search-input" placeholder="Search Booking"
                    aria-label="Search" aria-describedby="datatable-search-input" />
                <span class="input-group-text border-0" id="datatable-search-input">
                    <i class="fas fa-search"></i>
                </span>
            </div>
            <a href="{{ route('Coupons.create')}}" class="btn btn-success btn-sm btn-floating">
                <i class="fas fa-plus"></i>
            </a>
        </div>
    </div>
    <div class="container-fluid">
        <div class="table-responsive pb-3">
            <table class="table table-striped" id="dataTable" width="100%" cellspacing="0">
                <thead class="font-weight-bold text-title-color">
                    <th>#</th>
                    <th>Code coupon </th>
                    <th>Description</th>
                    <th>limit</th>
                    <th>date_debut</th>
                    <th>date_fin</th>
                </thead>
                <tbody>
                    @if($coupons->count() > 0)
                    @foreach($coupons as $rs)
                    <tr>
                        <td class="align-middle">{{ $loop->iteration }}</td>
                        <td class="align-middle">{{ $rs->code_coupon  }}</td>
                        <td class="align-middle">{{ $rs->description }}</td>
                        <td class="align-middle">{{ $rs->limit }}</td>
                        <td class="align-middle">{{\Carbon\Carbon::parse($rs->date_debut)->format('d/m/Y')}}</td>
                        <td class="align-middle">{{\Carbon\Carbon::parse($rs->date_fin)->format('d/m/Y')}}</td>
                        <td class="align-middle">
                            <div class="dropdown">
                                <a class="dropdown-toggle hidden-arrow" type="button" id="dropdownMenuicon"
                                    data-mdb-toggle="dropdown" aria-expanded="false">
                                    <i class="fas fa-ellipsis-h fa-lg text-dark"></i>
                                </a>
                                <ul class="dropdown-menu" aria-labelledby="dropdownMenuicon">
                                    <li>
                                        <a class="dropdown-item" href="{{ route('Coupons.show', $rs->id) }}"> <i
                                                class="fas fa-info-circle pe-2"></i>Details</a>
                                    </li>
                                    <li>
                                        <a class="dropdown-item" href="{{ route('Coupons.edit', $rs->id)}}"> <i
                                                class="fas fa-edit pe-2"></i>Edit</a>
                                    </li>
                                    <li>
                                        <form action="{{ route('Coupons.destroy', $rs->id) }}" class="dropdown-item"
                                            method="POST" id="deleteform">
                                            @csrf
                                            @method('DELETE')
                                            <div onclick="if (confirm('Delete?')) { document.getElementById('deleteform').submit()};"
                                                style="cursor: pointer;">

                                                <i class="fas fa-trash pe-2"></i> Delete
                                            </div>
                                        </form>
                                    </li>
                                </ul>
                            </div>
                        </td>
                    </tr>
                    @endforeach
                    @endif
                </tbody>
            </table>
        </div>
    </div>
</div>
<script src="{{ asset('admin_assets/mdb/js/mdb.min.js') }}"></script>
<script src='https://fullcalendar.io/js/fullcalendar-3.1.0/lib/jquery.min.js'></script>
<script>
$(document).ready(function() {
    var dataTable = $('#dataTable').DataTable({
        searching: true,
        lengthChange: false,
        info: false,
        columnDefs: [{
                searchable: false,
                orderable: false,
                targets: [6]
            } // Disable search on first and last columns
        ],
    });
    $('#datatable-search-input').change(function() {
        dataTable.search($(this).val()).draw();
    })
});
</script>
@endsection

****************edit blade *******************
@extends('layouts.app')

@section('title', 'Add Coupon')

@section('contents')
    <link href="{{ asset('admin_assets/mdb/css/mdb.min.css') }}" rel="stylesheet">

    <div class="row">
        <div class="col mx-auto mb-4">
            <form action="{{ route('Coupons.update', $Coupon->id) }}" method="POST" enctype="multipart/form-data">
                @csrf
                @method('PATCH')

                <div class="card mb-4">
                    <div class="card-header py-3 d-flex align-items-center justify-content-between">
                        <h5 class="mb-0">Update Coupon</h5>
                        <button type="submit" class="btn btn-success btn-floating">
                            <i class="fas fa-save"></i>
                        </button>
                    </div>
                    <div class="card-body">

                     
                      <div class="row mb-4">
                      @error('code_coupon')
                                        <p class="text-danger fs-9" >{{ $message }}</p>
                                    @enderror
                                <div class="col">
                                    <div class="form-outline">
                                            <input type="text" id="code_coupon" name="code_coupon"
                                                class="form-control form-control-lg active @error('code_coupon') is-invalid @enderror" value="{{$Coupon->code_coupon}}" required />
                                            <label class="form-label fw-bold" for="code_coupon">code_coupon </label>
                                        </div>
                                </div>
                                @error('limit')
                                        <p class="text-danger fs-9" >{{ $message }}</p>
                                    @enderror
                                <div class="col">
                                    <div class="form-outline">
                                            <input type="number" id="limit" name="limit" value="{{$Coupon->limit}}"
                                                class="form-control form-control-lg active @error('code_coupon') is-invalid @enderror" required />
                                            <label class="form-label fw-bold" for="limit">limit</label>
                                        </div>
                                </div>
                               
                            </div>
                            @error('limit')
                                        <p class="text-danger fs-9" >{{ $message }}</p>
                                    @enderror
                      <div class="row mb-4">
                                
                                <div class="col">
                                    <div class="">
                                    <input type="Date" class="form-control datepicker @error('code_coupon') is-invalid @enderror" id="date_debut" name="date_debut"  value="{{$Coupon->date_debut}}" >

                                        </div>
                                </div>
                                <div class="col">
                                    <div class="">
                                    <input type="date" class="form-control datepicker @error('code_coupon') is-invalid @enderror" id="date_fin" name="date_fin"  value="{{$Coupon->date_fin}}">

                                        </div>
                                </div>
                               
                            </div>
                            <div class="row mb-4">
                                
                            <div class="col">
                                    <label class="form-label fw-bold" for="description">Description</label>
                                    <textarea name="description" id="description" >{{$Coupon->description}}</textarea>
                                </div>
                            </div>
                         
           
                    </form>
       
        </div>
    </div>
    <script src="{{ asset('admin_assets/mdb/js/mdb.min.js') }}"></script>
 <script src='https://fullcalendar.io/js/fullcalendar-3.1.0/lib/jquery.min.js'></script>
<script src="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/js/select2.min.js" defer></script>
<script src="https://cdn.ckeditor.com/ckeditor5/40.1.0/classic/ckeditor.js"></script>
<script>
    ClassicEditor
        .create(document.querySelector('#description'))
        .catch(error => {
            console.error(error);
        });

    

</script>
@endsection
 
*******************create blade *******************
@extends('layouts.app')

@section('title', 'Add Coupon')

@section('contents')
    <link href="{{ asset('admin_assets/mdb/css/mdb.min.css') }}" rel="stylesheet">

    <div class="row">
        <div class="col mx-auto mb-4">
            <form action="{{ route('Coupons.store') }}" method="POST" enctype="multipart/form-data">
                @csrf
                <div class="card mb-4">
                    <div class="card-header py-3 d-flex align-items-center justify-content-between">
                        <h5 class="mb-0">Add Coupon</h5>
                        <button type="submit" class="btn btn-success btn-floating">
                            <i class="fas fa-save"></i>
                        </button>
                    </div>
                    <div class="card-body">

                     
                      <div class="row mb-4">
                                
                                <div class="col">
                                @error('code_coupon')
                                 <p class="text-danger fs-9" >{{ $message }}</p>
                                    @enderror
                                    <div class="form-outline">
                                
                                            <input type="text" id="code_coupon " name="code_coupon" 
                                                class="form-control form-control-lg active @error('code_coupon') is-invalid @enderror" required />
                                            <label class="form-label fw-bold" for="code_coupon ">code_coupon </label>
                                        </div>
                                </div>
                                @error('limit')
                                <p class="text-danger fs-9" >{{ $message }}</p>
                                    @enderror
                                <div class="col">
                              
                                    <div class="form-outline">
                                            <input type="number" id="limit" name="limit"
                                                class="form-control form-control-lg active @error('limit') is-invalid @enderror" required />
                                            <label class="form-label fw-bold" for="limit">limit</label>
                                        </div>
                                </div>
                               
                            </div>
                            
                      <div class="row mb-4">
                                 
                                <div class="col">
                                    <div class="">
                                    <input type="Date" class="form-control datepicker @error('date_debut') is-invalid @enderror" id="date_debut" name="date_debut" >
                                </div>

                                </div>
                                @error('date_fin')
                                <p class="text-danger fs-9" >{{ $message }}</p>
                                    @enderror
                                <div class="col">
                                    <div class="">
                                   
                                    
                                    <input type="date" class="form-control datepicker @error('date_fin') is-invalid @enderror" id="date_fin" name="date_fin" >

                                        </div>
                                </div>
                               
                            </div>
                            <div class="row mb-4">
                                
                            <div class="col">
                                    <label class="form-label fw-bold" for="description">Description</label>
                                    <textarea name="description" id="description"></textarea>
                                </div>
                            </div>
                         
           
                    </form>
       
        </div>
    </div>
    <script src="{{ asset('admin_assets/mdb/js/mdb.min.js') }}"></script>
 <script src='https://fullcalendar.io/js/fullcalendar-3.1.0/lib/jquery.min.js'></script>
<script src="https://cdn.jsdelivr.net/npm/select2@4.1.0-rc.0/dist/js/select2.min.js" defer></script>
<script src="https://cdn.ckeditor.com/ckeditor5/40.1.0/classic/ckeditor.js"></script>
<script>
    ClassicEditor
        .create(document.querySelector('#description'))
        .catch(error => {
            console.error(error);
        });

    

</script>
@endsection
*************************************** migrate 
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('coupons', function (Blueprint $table) {
            $table->id();
            $table->string('code_coupon')->unique();
            $table->text('description');
            $table->integer('limit');
            $table->date('date_debut');
            $table->date('date_fin');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::dropIfExists('coupons');
    }
};
 **************************coupon php model ****************
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Coupon extends Model
{
    use HasFactory;
    protected $fillable = [
        'code_coupon',
        'description',
            'limit',
            'date_debut',
            'date_fin',
    ];   
    
}
**************************** controler ***********
<?php

namespace App\Http\Controllers;
use App\Models\Coupon;
use Carbon\Carbon;

use Illuminate\Http\Request;

class CouponsController extends Controller
{
    /**
     * Display a listing of the resource.
     */
    public function index()
    {
        //
        $coupons = Coupon::orderBy('created_at', 'DESC')->get();
        return view('coupon.index', compact('coupons'));
    }

    /**
     * Show the form for creating a new resource.
     */
    public function create()
    {
        //
        return view('coupon.create');

    }

    /**
     * Store a newly created resource in storage.
     */
    public function store(Request $request)
    {
        //
        $validated = $request->validate([
            'code_coupon' => ['required', 'unique:coupons', 'max:11'],
            'limit' => ['required', 'max:10', 'regex:/^[0-9]+$/'],
            'description' => ['required', 'max:300'],
            'date_debut' => ['required'],
            'date_fin' => ['required', 'after:date_debut'],
        ]);

            $coupon = new Coupon();
            $coupon->code_coupon=$request->input('code_coupon');
            $coupon->limit=$request->input('limit');
           
             $coupon->description=strip_tags($request->input('description'));
            $coupon->date_debut = Carbon::createFromFormat('Y-m-d', $request->input('date_debut')); 
            $coupon->date_fin = Carbon::createFromFormat('Y-m-d', $request->input('date_fin')); 

            if ($coupon->date_fin->gt($coupon->date_debut)) { // Check if date_debut is greater than date_fin
                $coupon->save();
            } 
            return redirect()->route('Coupons')->with('success', 'Coupon added successfully');
        
    }

    /**
     * Display the specified resource.
     */
    public function show(string $id)
    {
        $Coupon = Coupon::findOrFail($id);
  
        return view('coupon.show', compact('Coupon'));
    }

    /**
     * Show the form for editing the specified resource.
     */
    public function edit(string $id)
    {
        $Coupon = Coupon::findOrFail($id);
  
        return view('coupon.edit', compact('Coupon'));
    
    }

    /**
     * Update the specified resource in storage.
     */
    public function update(Request $request, string $id)
    {
        $coupon = Coupon::findOrFail($id);
        $validated = $request->validate([
            'code_coupon' => ['required', 'max:11'],
            'limit' => ['required', 'max:10', 'regex:/^[0-9]+$/'],
            'description' => ['required', 'max:300'],
            'date_debut' => ['required'],
            'date_fin' => ['required', 'after:date_debut'],
        ]);
        
        $coupon->update([
            'code_coupon'=>$request->code_coupon,
            'limit'=>$request->limit,
            'description'=>strip_tags($request->description),
            'date_fin'=>$request->date_fin,
            'date_debut'=>$request->date_debut,
        ]);
         return redirect()->route('Coupons')->with('success', 'Coupons updated successfully');   
     }

    /**
     * Remove the specified resource from storage.
     */
    public function destroy(string $id)
    {
        $Coupon = Coupon::findOrFail($id);
  
        $Coupon->delete();
  
        return redirect()->route('Coupons')->with('success', 'Coupons deleted successfully');    }
}
***************************************************************************
************************************************************************
***************************************************************************
******************************************************************************
php artisan serve --port=8888
create table (new file migration) :php artisan make:migration create_new_table
modifie file
+migrate 
php artisan migrate
create model  
php artisan make:model NewTable
create controller and generate methods
php artisan make:controller PromotionCardController --resource 
if you want to chaange chi haja f file migrate use
php artisan make:migration update_promotion_cards --table=promotion_cards

old functions (if refrech keep old values in input) b9a 3a9l 3lih 
discard all delete changes
$ php artisan make:request PromotionCard is form optmisation code 





users 3lach fiha id account o organisation
ornaisation mfihach id super admin
