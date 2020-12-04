```javascript
import { Component, OnInit } from '@angular/core';
import { ModalDismissReasons, NgbModal } from '@ng-bootstrap/ng-bootstrap';


@Component({
  selector: 'app-modal',
  templateUrl: './modal.component.html',
  styleUrls: ['./modal.component.css']
})
export class ModalComponent implements OnInit {

  closeResult: string;

  constructor(private modalService: NgbModal) { }

  open(content) {
    this.modalService.open(content, {ariaLabelledBy: 'modal-basic-title'}).result.then((result) => {
      this.  = `Closed with: ${result}`;
    }, (reason) => {
      this.closeResult = `Dismissed ${this.getDismissReason(reason)}`;
    });
  }

   private getDismissReason(reason: any): string {
    if (reason === ModalDismissReasons.ESC) {
      return 'by pressing ESC';
    } else if (reason === ModalDismissReasons.BACKDROP_CLICK) {
      return 'by clicking on a backdrop';
    } else {
      return  `with: ${reason}`;
    }
  }

  ngOnInit(): void {
  }

}

````
```html
<button class="btn btn-primary" (click)="open(reportmodal)">Open Modal</button>

<ng-template #reportmodal let-modal>
  <div class="modal-header">
    <h4 class="modal-title" id="modal-basic-title">Patient Report</h4>
  </div>

  <div class="modal-body">
    <form>
      <div class="form-group">
        <label for="ReportType">Issue</label>
        <input type="text" class="form-control" name="ReportForm" placeholder="Issue">
      </div>
      <div class="form-row mb-1">
      <div class="col-md-6 form-group">
        <label for="Type">Type</label>
        <div>
          <input type="radio" (click)="OPD_fun()" name="type" value="OPD"> OPD
          <input type="radio" (click)="IPD_fun()" name="type" value="IPD"> IPD
        </div>
      </div>
      <div *ngIf="IPD_variable" class="col-md-6 form-group">
        <label for="Discharge">Discharge Date</label>
        <div class="input-group">
          <input id="Discharge" class="form-control" placeholder="yyyy-mm-dd" name="Discharge" ngbDatepicker #dp="ngbDatepicker">
          <div class="input-group-append">
            <button class="btn btn-outline-secondary" (click)="dp.toggle()" type="button"><i class="fa fa-calendar" aria-hidden="true"></i></button>
          </div>
        </div>
      </div>
      </div>
      <div class="form-group">
        <label for="ReportType">Summary</label>
        <textarea rows="4" cols="50" class="form-control" id="patientAppointmentForm" name="patientAppointmentForm" placeholder="Add Your summary here"></textarea>
      </div>
      <label for="Discharge">Lab Reports</label>
      <button class="ml-2 btn btn-primary">Assign</button>
      <div class="form-group mt-2">
        <label for="ReportType">Upload Paper Report (optional)</label>
        <input type="file" class="form-control" name="ReportUpload">
      </div>
    </form>
  </div>
  <div class="modal-footer">
    <button type="button" class="btn btn-success" (click)="modal.close('Save click')">Save</button>
    <button type="button" class="btn btn-danger" (click)="modal.close('Save click')">Close</button>
  </div>

</ng-template>

```

